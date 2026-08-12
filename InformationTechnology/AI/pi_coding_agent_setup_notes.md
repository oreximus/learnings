# Pi Coding Agent — Full Setup Notes (Updated)

**Last updated:** 2026-08-13
**Model in use:** `deepseek/deepseek-v4-flash` via provider `commandcode`

**Stack covered:**
1. `pi-observational-memory` — long-session memory / fast compaction
2. `pi-minimal-subagent` (+ `pi-fork`) — named subagents with clean context
3. `pi-codemapper` — structural code navigation
4. `pi-rtk-optimizer` — command rewriting + tool-output compaction

---

## 0. The big picture

| Problem | Solved by |
|---|---|
| Main agent context gets noisy / polluted with exploration | `pi-minimal-subagent` / `pi-fork` — delegate to subagents with clean, separate context |
| Main agent forgets *why* decisions were made across days/compactions | `pi-observational-memory` — background observation + reflection capture, fast compaction |
| Reading whole files to find one function wastes tokens | `pi-codemapper` — structural navigation (map/search/outline/expand/path) instead of blind reads |
| Routine tool output (builds, git, tests, greps) is mostly noise | `pi-rtk-optimizer` — compaction pipeline + `rtk` command rewriting |

**Why memory + subagents is the real force-multiplier:** observational memory keeps the *main* agent's context rich across weeks of work; subagents keep exploration noise *out* of that main context in the first place. Codemapper and rtk-optimizer both reduce token cost per action, so what does land in context is dense with signal instead of raw logs.

---

## 1. Where each plugin's config actually lives

This trips people up, so it's worth stating plainly before anything else:

| Extension | Config location | Scope |
|---|---|---|
| `pi-observational-memory` | `.pi/settings.json` (project) or `~/.pi/agent/settings.json` (global) | project overrides global |
| `pi-minimal-subagent` | same `.pi/settings.json` file, different namespace key | project overrides global |
| `pi-codemapper` | **no settings.json entry** — env var only (`CODEMAPPER_BIN`), or auto-detected on `PATH` / `~/.local/bin/cm` | launch-time, not project-scoped |
| `pi-rtk-optimizer` | its own dedicated `config.json` under the extension's install folder | not project-scoped by default |

Only two of the four extensions actually share a settings file. The other two are configured completely differently — don't go looking for `pi-codemapper` or `pi-rtk-optimizer` keys inside `.pi/settings.json`, they aren't there.

---

## 2. `pi-observational-memory`

### What it does
- **Observations**: concrete, timestamped things that happened (decisions, completed work, bugs traced, constraints stated), each with a 12-char id.
- **Reflections**: durable facts *distilled from* observations (tech stack, deadlines, preferences).
- **Dropper**: prunes old active observations once safely covered by a reflection or superseded — doesn't delete ledger history.
- **`recall` tool**: pulls original source evidence for a specific id.
- Memory work happens continuously in the background, so compaction is a **fast render**, not a slow rewrite.

### Requirements
Pi **0.81.0+**.

### Install
```bash
pi install npm:pi-observational-memory
```

### Commands
| Command | Use |
|---|---|
| `/om:status` | Memory counts, drift, pool pressure, worker state, last errors |
| `/om:view` | Shows + copies current visible memory |
| `/om:view full` | Full memory state (use before first V3 compaction — visible memory can be empty until then) |
| `recall <id>` (agent tool) | Pulls original source evidence for a specific id |

### ⚠️ V3 migration
Not backward-compatible with V2. Old V2 settings are **silently ignored** (falls back to defaults, no error). Start a fresh Pi session after upgrading.

---

## 3. `pi-minimal-subagent` (and `pi-fork`)

### What it does
Registers **one tool**, `subagent`. No built-in parallel/chain/pool/orchestrator — deliberately minimal. Parallelism happens because Pi executes multiple tool calls in the same turn concurrently.

### Install
```bash
pi install git:github.com/elpapi42/pi-minimal-subagent
```

### Defining agents
Markdown + YAML frontmatter, no registration step:
```markdown
---
name: scout
description: Fast codebase reconnaissance
model: commandcode/deepseek/deepseek-v4-flash
---
You are a fast codebase scout. Return dense findings for the parent agent.
```
Loaded from `~/.pi/agent/agents/*.md` (global) and `.pi/agents/*.md` (project — overrides global on name collision).

Supported frontmatter: `model`, `extensions`, `skills`, `thinking`. **Not** `tools` — subagents always inherit Pi's default enabled tools.

### Recommended roles
```markdown
---
name: advisor
description: Strategic/architecture sounding board, no code edits
model: commandcode/deepseek/deepseek-v4-flash
thinking: high
---
You give architecture and product-strategy opinions. You do not edit code.
Push back on the main agent's plan if there's a better structural approach.
```
```markdown
---
name: reviewer
description: Code quality, security, and UX review of recent changes
model: commandcode/deepseek/deepseek-v4-flash
thinking: medium
---
You review diffs for correctness, security issues, and UX regressions.
Be specific: file, line, severity, fix suggestion.
```

### Usage
```
> Use the scout agent to inspect the auth flow and report risks.
> Spawn scout on three tasks in parallel: auth module, payment module, rate limiter.
> Have the reviewer look at the diff for security and code quality before I open the PR.
> Ask the advisor whether this abstraction is the right call before I refactor processPayment.
```

### Things to know
- No per-agent tool restriction beyond the `extensions` tri-state.
- Recursion is **allowed, not blocked**.

---

## 4. `pi-codemapper`

> ⚠️ **Known issue:** the underlying `codemapper` binary (`p1rallels/codemapper`) is reportedly unmaintained with a cache bug requiring manual patching. `cymbal` is being watched as a potential future replacement.

### The five tools
| Tool | Answers | Use before |
|---|---|---|
| `map({ path? })` | "What is here?" | broad `find`/`ls` sweeps |
| `search({ query, path?, exact? })` | "Where is X?" (fuzzy, **not** semantic) | reading files blindly |
| `outline({ file })` | "What's inside this file?" (no function bodies) | reading the whole file |
| `expand({ symbol })` | "What's connected to this symbol?" | editing/renaming/deleting it |
| `path({ from, to })` | "Is there a static call path A→B?" | tracing runtime flow |

All tools return raw CodeMapper data only — no scores, no summaries. Output is always: JSON array (success), `[]` (no results), or plain-string error.

### Installing the `cm` binary itself (required prerequisite — easy to miss)
`cm` is not something `pi install` fetches for you. It's a separate Rust CLI you build yourself:

```bash
# 1. Requires Rust/Cargo — check first:
cargo --version
# if missing: curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# 2. Build and install
git clone https://github.com/p1rallels/codemapper.git
cd codemapper
cargo build --release
mkdir -p ~/.local/bin
cp target/release/cm ~/.local/bin/cm

# 3. Put ~/.local/bin on PATH (zsh)
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# 4. Verify
cm --help
cm stats . --format ai
```
Once `cm --help` works, `pi-codemapper` finds it automatically at `~/.local/bin/cm` — no env var needed.

### Install the Pi extension
```bash
pi install git:git@github.com:elpapi42/pi-codemapper.git
```
Requires SSH access to the repo. Restart Pi or `/reload`; confirm with `pi list`.

### Configuration (env var only, launch-time)
```bash
CODEMAPPER_BIN=/absolute/path/to/cm pi -e git:git@github.com:elpapi42/pi-codemapper.git
```
Resolution order: `CODEMAPPER_BIN` → `~/.local/bin/cm` → `cm` on `PATH`. Only needed if the binary isn't already discoverable via the two automatic paths.

**Tool-name collision:** registers a generic `search` tool. If also running something else that registers `search` (e.g. `pi-cocoindex`), **load order decides which wins silently**.

### Cache troubleshooting
```bash
rm -rf .codemapper
cm stats . --rebuild-cache
```

---

## 5. `pi-rtk-optimizer`

### What it does
1. **Command rewriting** — rewrites `bash` calls to `rtk` equivalents, delegating entirely to the installed `rtk` binary (`rtk rewrite`).
2. **Output compaction pipeline** — ANSI stripping, test/build/git/linter/search aggregation, optional source filtering, smart/hard truncation. Anchor-safe for Pi's hashline edit markers.

### Installing the `rtk` binary itself (separate from the Pi extension — also easy to miss)
```bash
curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
rtk --version
```
Also install `ripgrep` if not already present (`rtk` shells out to it for some filters):
```bash
brew install ripgrep   # macOS
# or: sudo apt install ripgrep   # Linux
```

### Install the Pi extension
```bash
pi install npm:pi-rtk-optimizer
```

### Commands
| Command | Does |
|---|---|
| `/rtk` | Interactive TUI settings modal |
| `/rtk show` | Current config + runtime status |
| `/rtk verify` | Checks `rtk` binary resolvable |
| `/rtk stats` | Compaction savings this session |
| `/rtk clear-stats` / `/rtk reset` | Reset metrics / config |

### If you see: `rtk binary unavailable, command rewrite bypassed`
Non-fatal (`guardWhenRtkMissing: true` means commands still run raw) — but fix it by installing `rtk` per above, then confirm with `/rtk verify`.

### Config file location
```text
~/.pi/agent/extensions/pi-rtk-optimizer/config.json
```

---

## 6. Final config files (all in one place, corrected provider)

### `.pi/settings.json` (project root — covers memory + subagents)
```json
{
  "observational-memory": {
    "observeAfterTokens": 10000,
    "reflectAfterTokens": 20000,
    "compactAfterTokens": 81000,
    "compactAfterTokensMode": "calibrated",
    "compactAfterTokensRatio": 0.68,
    "observationsPoolMaxTokens": 20000,
    "observationsPoolTargetTokens": 10000,
    "agentMaxTurns": 16,
    "model": {
      "provider": "commandcode",
      "id": "deepseek/deepseek-v4-flash",
      "thinking": "low"
    },
    "showWorkerNotifications": true,
    "passive": false,
    "debugLog": false
  },

  "pi-minimal-subagent": {
    "model": "commandcode/deepseek/deepseek-v4-flash",
    "extensions": [],
    "environment": {}
  }
}
```

### `~/.pi/agent/extensions/pi-rtk-optimizer/config.json`
```json
{
  "enabled": true,
  "mode": "suggest",
  "guardWhenRtkMissing": true,
  "showRewriteNotifications": true,
  "outputCompaction": {
    "enabled": true,
    "stripAnsi": true,
    "readCompaction": { "enabled": false },
    "sourceCodeFilteringEnabled": false,
    "preserveExactSkillReads": true,
    "sourceCodeFiltering": "none",
    "aggregateTestOutput": true,
    "filterBuildOutput": true,
    "compactGitOutput": true,
    "aggregateLinterOutput": true,
    "groupSearchOutput": true,
    "trackSavings": true,
    "smartTruncate": { "enabled": false, "maxLines": 220 },
    "truncate": { "enabled": true, "maxChars": 12000 }
  }
}
```

### `pi-codemapper` — no file, launch-time env var only
```bash
# only needed if cm isn't already on PATH or at ~/.local/bin/cm
CODEMAPPER_BIN=/absolute/path/to/cm pi
```

---

## 7. Harness context (background)

Six components every serious agent system implements: task definition, context/memory manager, tool execution layer, loop controller, verification layer, failure handler. **Pi gives you steps 3–6 as infrastructure on day one** — you still supply steps 1–2 (task + verification) yourself; `pi-observational-memory` strengthens step 2 but doesn't replace defining "done."

- `AGENTS.md` — project instructions loaded at startup from `~/.pi/agent`, parent dirs, and cwd.
- `SYSTEM.md` — replaces/appends Pi's default system prompt *per project*.

---

## 8. Production scenario — multi-day feature build, this stack end-to-end

Concrete walkthrough of what a real feature ticket looks like using all four extensions together, with the corrected `commandcode` provider config in place.

### Day 1 — orientation, ticket kickoff
```
> We're adding a refund flow to checkout. Map this repo and find everything
> related to payments and checkout before we touch anything.
```
- `pi-codemapper`'s `map({path:"."})` gives structure without full reads; if the repo's large, it returns a `notice` pointing at narrower directories instead of failing.
- `search({query:"checkout|payment|refund", path:"src"})` surfaces relevant files by symbol/term, not semantic guessing.
- `pi-observational-memory` silently starts recording: *"Ticket: add refund flow to checkout. Scope: src/payments, src/checkout."* — this becomes the anchor reflection for the whole branch.

### Day 1 — architecture sanity check before writing code
```
> Before we start, spawn the advisor to review whether a new RefundService
> class or extending PaymentService is the better call.
```
- `pi-minimal-subagent` spawns `advisor` on `commandcode/deepseek/deepseek-v4-flash` with a **clean context** — it only sees the task you hand it, not your whole exploration history, so its opinion isn't anchored to your own framing.
- Decision gets recorded as an observation automatically; the *reasoning* behind it (not just the conclusion) survives compaction later.

### Day 2–3 — implementation, using expand before every risky edit
```
> I need to modify processPayment to support partial refunds.
> Use expand first to check what depends on it.
```
- `expand({symbol:"processPayment"})` returns exact definition, callers, callees, and detected tests in one call — no guessing what breaks.
- While this runs, `pi-rtk-optimizer` is compacting test output, build logs, and git diffs in the background automatically — you don't invoke it, it just keeps `npm test` runs from flooding context. Occasionally check:
```
/rtk stats
```

### Day 3 — mid-session, context getting long
```
/om:status
```
Check pool pressure. Because memory work has been running continuously in the background, when Pi's actual compaction trigger fires, it's a fast render — you likely won't notice the pause that used to happen on long sessions.

### Day 4 — code review before opening the PR
```
> Have the reviewer check the refund flow diff for security and code quality issues.
```
- `reviewer` subagent, also on the DeepSeek flash model, runs in a clean context so it's evaluating the diff on its own merits — not biased by having "written" the code across the last three days of back-and-forth.

### Day 6 — picking the branch back up after a few days away
```
> /om:view full
```
Reloads the full decision history: the RefundService-vs-extend decision, the constraint that partial refunds must not touch the existing full-refund path, what's already been tested. No re-explaining the ticket from scratch, no risk of the agent re-litigating a decision that was already settled on Day 1.

### Day 6 — final trace check before merge
```
> Is there a call path from the new refund endpoint to processPayment
> that could double-charge a customer?
```
- `path({from:"refundHandler", to:"processPayment"})` gives a detected static call path if one exists. If it returns `[]`, that's a signal to check manually — not proof it's safe, since dynamic dispatch and framework routing aren't caught.

### Why this is faster than working without the stack
- No re-reading whole files to relocate `processPayment` each time (`codemapper`)
- No re-explaining "why we chose RefundService" three days later (`observational-memory`)
- No polluting your main context with the advisor's/reviewer's back-and-forth exploration (`subagent`)
- No burning tokens on raw `npm test` and `git diff` output during a long implementation session (`rtk-optimizer`)

---

## 9. Corrections applied in this revision
- Provider name corrected: **`commandcode`** (not `commandcode-provider`) — updated in both `observational-memory.model.provider` and `pi-minimal-subagent.model` / agent frontmatter strings.
- Added the missing prerequisite installs for the two external binaries (`cm` and `rtk`) that the Pi extensions depend on but don't install themselves.
- Clarified config-file locations per extension (Section 1) to prevent looking for settings in the wrong file.
