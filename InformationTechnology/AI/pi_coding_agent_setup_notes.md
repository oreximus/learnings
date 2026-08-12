# Pi Coding Agent — Full Setup Notes

**Last updated:** 2026-08-13

**Stack covered:**
1. `pi-observational-memory` — long-session memory / fast compaction
2. `pi-minimal-subagent` (+ `pi-fork`) — named subagents with clean context
3. `pi-codemapper` — structural code navigation
4. `pi-rtk-optimizer` — command rewriting + tool-output compaction

**Original sources:**
- r/PiCodingAgent setup thread
- explainx.ai — Pi minimal agent harness guide (Mario Zechner)
- README files for each extension (as of this doc's date)

---

## 0. The big picture

These four extensions solve two different problems, and the combination is the actual value:

| Problem | Solved by |
|---|---|
| Main agent context gets noisy / polluted with exploration | `pi-minimal-subagent` / `pi-fork` — delegate to subagents with clean, separate context |
| Main agent forgets *why* decisions were made across days/compactions | `pi-observational-memory` — background observation + reflection capture, fast compaction |
| Reading whole files to find one function wastes tokens | `pi-codemapper` — structural navigation (map/search/outline/expand/path) instead of blind reads |
| Routine tool output (builds, git, tests, greps) is mostly noise | `pi-rtk-optimizer` — compaction pipeline + `rtk` command rewriting |

**Why memory + subagents is the real force-multiplier:** observational memory keeps the *main* agent's context rich and relevant across weeks of work; subagents keep exploration noise *out* of that main context in the first place. Codemapper and rtk-optimizer both reduce token cost per action, so what does land in context is dense with signal instead of raw logs.

Result (per original notes): a personal agent setup that "never forgets" and stays useful for weeks before the context window gets maxed out.

---

## 1. `pi-observational-memory`

> Custom compaction system inspired by [Mastra's Observational Memory research](https://mastra.ai/blog/observational-memory). Makes long Pi sessions feel endless by preparing memory continuously instead of summarizing in a slow burst at compaction time.

### What it does
- **Observations**: concrete, timestamped things that happened during the session (decisions, completed work, bugs traced, constraints stated), each with a 12-char id.
- **Reflections**: durable facts *distilled from* observations (tech stack, deadlines, project preferences) — meant to survive long-term.
- **Dropper**: prunes old active observations once safely covered by a reflection, superseded, or redundant — without deleting ledger history.
- **`recall` tool**: lets the agent pull original source evidence for a specific observation/reflection id when a compressed memory isn't precise enough to act on.
- Memory work happens continuously in the background (`turn_end`), so when compaction actually triggers (`agent_settled` → threshold), it's a **fast render** of already-prepared memory, not a slow rewrite.

### Requirements
Pi **0.81.0+** (needs `agent_settled` lifecycle event).

### Install
```bash
pi install npm:pi-observational-memory
```

### Configuration
Settings under `observational-memory` in `~/.pi/agent/settings.json` (global) or `.pi/settings.json` (project overrides global).

**Recommended starting config** (defaults are sane for most users):
```json
{
  "observational-memory": {
    "observeAfterTokens": 10000,
    "reflectAfterTokens": 20000,
    "compactAfterTokens": 81000,
    "compactAfterTokensMode": "calibrated",
    "observationsPoolMaxTokens": 20000,
    "observationsPoolTargetTokens": 10000,
    "agentMaxTurns": 16,
    "showWorkerNotifications": true,
    "passive": false,
    "debugLog": false
  }
}
```

**Two settings worth tuning deliberately:**

1. **Large-context models (≥500K–1M tokens):** switch to ratio mode so compaction scales with the model's actual window instead of firing at a fixed ~81K:
   ```json
   {
     "observational-memory": {
       "compactAfterTokensMode": "ratio",
       "compactAfterTokensRatio": 0.68
     }
   }
   ```
   Threshold = `floor(contextWindow * ratio)`. Lower the ratio (~0.4) for models with big windows but weak long-range attention; raise it (~0.7) for models that stay sharp deep into context.

2. **Cheaper background memory work:** point the memory *worker* (observer/reflector/dropper) at a lighter model than your main coding model:
   ```json
   {
     "observational-memory": {
       "model": { "provider": "openrouter", "id": "google/gemma-4-31b-it", "thinking": "low" }
     }
   }
   ```
   Without this, memory workers use your session model — fine, but pricier since memory work runs constantly.

### Commands / tool
| Command | Use |
|---|---|
| `/om:status` | Memory counts, visible/full drift, pool pressure, worker state, last errors |
| `/om:view` | Shows + copies current visible memory |
| `/om:view full` | Full memory state (visible memory can be empty before the first V3 compaction — use this to check what's actually recorded) |
| `recall <id>` (agent tool) | Pulls original source evidence for a specific observation/reflection id |

### ⚠️ V3 migration note
V3 is **not backward-compatible** with V2. If old V2 settings are still present, they're **silently ignored** (not an error) — V3 falls back to defaults. Key renames: `observationThresholdTokens` → `observeAfterTokens`, `compactionModel` → `model`, `thinkingLevel` → `model.thinking`. Start a **fresh Pi session** after upgrading — old sessions may still show stale V2-era compaction text until a new V3 compaction runs.

---

## 2. `pi-minimal-subagent` (and `pi-fork`)

> Minimal named-subagent tool. `pi-fork` is a sibling/earlier concept described as "basic and minimalist" — same core idea (subagents that share the main agent's extension context but run isolated). Treat the guidance below as applying to whichever one is actually installed.

### What it does
Registers **one tool**, `subagent`, that spawns a named agent to do a task:
```json
{ "agent": "scout", "task": "Inspect the auth flow and report risks." }
```
No built-in parallel/chain/pool/orchestrator modes — deliberately minimal. Parallelism happens because Pi executes multiple tool calls in the same turn concurrently; you just ask the parent agent to issue several `subagent` calls at once.

**Core value (per original notes):** the main agent's context stays rich and dense per token because exploration noise stays inside the subagent's clean, separate context.

### Install
```bash
pi install git:github.com/elpapi42/pi-minimal-subagent
```
Restart Pi or `/reload`.

### Defining agents
Markdown files with YAML frontmatter, no registration step needed:
```markdown
---
name: scout
description: Fast codebase reconnaissance
model: claude-haiku-4-5
extensions: npm:some-pi-extension
---
You are a fast codebase scout. Return dense findings for the parent agent.
```
Loaded from:
- Global: `~/.pi/agent/agents/*.md` (honors `PI_CODING_AGENT_DIR`)
- Project: `.pi/agents/*.md` (current project or ancestor dir) — **overrides** global agent of the same name

Supported frontmatter: `model`, `extensions`, `skills`, `thinking`. **Not** `tools` — subagents always inherit Pi's default enabled tools.

### Configuration
Settings under `pi-minimal-subagent` in `~/.pi/agent/settings.json` / `.pi/settings.json`:
```jsonc
{
  "pi-minimal-subagent": {
    "model": "claude-haiku-4-5",  // cheap default; override per-agent for heavier tasks
    "extensions": [],              // subagents start bare — no accidental heavy tooling
    "environment": {}               // add only what specific subagent extensions need
  }
}
```
- `model`: default model for spawned subagents; agent frontmatter `model` overrides it. Recommended pattern: cheap default (e.g. `claude-haiku-4-5`), stronger model set per-agent only where needed (e.g. `reviewer`).
- `extensions` (tri-state — the main gotcha):
  | Value | Behavior |
  |---|---|
  | `null` / omitted | Subagents load normal Pi extensions (same as parent) |
  | `[]` | Subagents run bare, `--no-extensions` |
  | non-empty array | Subagents run `--no-extensions`, then load only the listed ones |

  Recommended: `[]` or an explicit array for narrow-purpose agents like `scout` — don't let them inherit the full parent toolkit. Agent-frontmatter `extensions` are always appended on top regardless of mode.
- `environment`: env vars merged on top of the parent's already-inherited environment (project overrides global on conflict). **Not** a secrets/isolation mechanism — plain injection only.

### Recommended roles (matches your actual setup)
Two agents, both spawned with clean context so their opinions are less biased by the main session's accumulated noise:

```markdown
---
name: advisor
description: Strategic/architecture sounding board, no code edits
model: claude-sonnet-5
thinking: high
---
You give architecture and product-strategy opinions. You do not edit code.
Push back on the main agent's plan if there's a better structural approach.
```

```markdown
---
name: reviewer
description: Code quality, security, and UX review of recent changes
model: claude-sonnet-5
thinking: medium
---
You review diffs for correctness, security issues, and UX regressions.
Be specific: file, line, severity, fix suggestion.
```

### Usage examples
No slash commands — these are agent tools invoked by Pi from natural language:
```
> Use the scout agent to inspect the auth flow and report risks.
> Spawn scout on three tasks in parallel: auth module, payment module, rate limiter. Summarize together.
> Have the reviewer look at the diff for security and code quality before I open the PR.
> Ask the advisor whether this abstraction is the right call before I refactor processPayment.
```

### Things to know
- No per-agent tool restriction — subagents get whatever Pi's default tools are, scoped only via the `extensions` tri-state.
- Recursion is **allowed, not blocked** — a subagent can spawn nested subagents.

---

## 3. `pi-codemapper`

> Wraps the [CodeMapper](https://github.com/p1rallels/codemapper) CLI (`cm`) as five narrow agent tools. Goal: reduce the search space before the agent reads files, edits code, or runs tests.

> ⚠️ **Known issue (from original notes):** the underlying `codemapper` binary is reportedly unmaintained with a cache bug that required manual patching. [`cymbal`](https://github.com/1broseidon/cymbal) is being watched as a potential future replacement/backend — worth checking its maturity periodically.

### The five tools
| Tool | Answers | Use before |
|---|---|---|
| `map({ path? })` | "What is here?" | broad `find`/`ls` sweeps |
| `search({ query, path?, exact? })` | "Where is X?" (fuzzy/case-insensitive, **not** semantic) | reading files blindly |
| `outline({ file })` | "What's inside this file?" (no function bodies) | reading the whole file |
| `expand({ symbol })` | "What's connected to this symbol?" (definition, callers, callees, tests) | editing/renaming/deleting it |
| `path({ from, to })` | "Is there a detected static call path A→B?" | tracing runtime flow |

All tools return **raw CodeMapper data only** — no relevance scores, no summaries, no inferred explanations. Output is always one of: JSON array (success), `[]` (no results), or plain-string error.

### Prerequisites
```bash
cm --help
cm stats . --format ai
```
Resolution order for the binary: `CODEMAPPER_BIN` env var → `~/.local/bin/cm` → `cm` on `PATH`.

### Install
```bash
pi install git:git@github.com:elpapi42/pi-codemapper.git
```
Requires SSH access to the repo. Restart Pi or `/reload`; confirm with `pi list`.

### Configuration
Main lever is pointing at the right binary:
```bash
CODEMAPPER_BIN=/home/whitman/.local/bin/cm pi -e git:git@github.com:elpapi42/pi-codemapper.git
```
Set this if Pi's runtime `PATH` doesn't include `cm`, or to pin a specific build. Simplest fix long-term: install `cm` at `~/.local/bin/cm` so it's found automatically.

**Tool-name collision to watch:** registers a generic `search` tool. If also running `pi-cocoindex` (or anything else registering `search`), **extension load order decides which wins silently**. Be deliberate about load order, or rename one at the extension-code level.

### Recommended agent workflows
- **Unknown repo:** `map` → `search` domain terms from the map → `outline` likely files → targeted reads
- **Known feature area:** `search({query:"checkout|payment|charge", path:"src"})` → `outline` → read only relevant line ranges
- **Before any symbol edit:** always `expand({symbol})` first — definitions, callers, callees, tests in one call
- **Flow questions:** `path({from, to})`, fall back to manual investigation if `[]` (doesn't prove impossibility — dynamic dispatch/DI/macros can be missed)
- **Docs/API lookup:** `search({query:"/v1/orders", path:"docs"})` → `outline({file:"docs/api.md"})`

### Troubleshooting
| Symptom | Fix |
|---|---|
| `cm command was not found` | verify `cm --help`; set `CODEMAPPER_BIN` or install to `~/.local/bin/cm` |
| Tool not visible | restart / `/reload`, check `pi list` |
| `search` behaves like a different tool | another extension registered `search` — check load order |
| `No exact symbol found: X` | run `search({query:"X"})` first to get the real name |
| `[]` from `path` | may still be a real runtime path missed by static analysis |
| Output too large (>1000KB cap) | narrow `path`, tighten `query`, or use `outline` on a specific file |
| Stale results | `rm -rf .codemapper && cm stats . --rebuild-cache` |

---

## 4. `pi-rtk-optimizer`

> RTK command rewriting + tool-output compaction. Per original notes: "a classic, not much to say here, it saves some tokens."

### What it does
1. **Command rewriting** — rewrites `bash` calls to `rtk` equivalents. Delegates entirely to the installed `rtk rewrite` binary (RTK is the source of truth for supported commands/parsing — no duplicate rewrite logic in the extension itself, as of 0.6.0's breaking change removing per-category toggles).
2. **Output compaction pipeline** — ANSI stripping, test-result aggregation, build-error filtering, git output condensing, linter aggregation, search-result grouping, optional source-code filtering, smart/hard truncation. Anchor-safe: preserves Pi's hashline/edit-anchor prefixes so compaction doesn't break `str_replace`-style edits.

### Install
```bash
pi install npm:pi-rtk-optimizer
```
Or drop the folder into `~/.pi/agent/extensions/pi-rtk-optimizer` (auto-discovered).

### Commands
| Command | Does |
|---|---|
| `/rtk` | Interactive TUI settings modal, live editing, no restart |
| `/rtk show` | Current config + runtime status |
| `/rtk path` | Config file path |
| `/rtk verify` | Checks `rtk` binary is resolvable |
| `/rtk stats` | Compaction savings this session |
| `/rtk clear-stats` | Reset metrics |
| `/rtk reset` | Reset config to defaults |
| `/rtk help` | Usage help |

### Optimal configuration
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
    "aggregateTestOutput": true,
    "filterBuildOutput": true,
    "compactGitOutput": true,
    "aggregateLinterOutput": true,
    "groupSearchOutput": true,
    "trackSavings": true,
    "truncate": { "enabled": true, "maxChars": 12000 }
  }
}
```

**Two decisions that actually matter:**
1. **`mode`** — start on `"suggest"` (notify-only) for a session or two to see what it *would* rewrite before trusting `"rewrite"` (auto). `guardWhenRtkMissing: true` keeps commands running raw if the `rtk` binary ever goes missing, instead of breaking the session.
2. **`readCompaction.enabled`** — defaults to `false`, **leave it there while actively editing code**. Lossy compaction on `read` output is the one setting that can cause real harm: if the agent edits against a filtered view of a file, `str_replace`-style edits fail with "old text does not match." The README documents a recovery flow (disable → re-read → edit → re-enable). Since `pi-codemapper`'s `outline` already gives lossless structural views, there's little reason to turn this on at all in this stack.

Also set `preserveExactSkillReads: true` if using Pi skills — keeps skill-directory reads exact regardless of other settings.

**For audit/debugging sessions:** keep `showRewriteNotifications` on and read compaction off before gathering evidence — you want to see exactly what the agent saw, unfiltered.

### Notes
- Peer deps: `@earendil-works/pi-coding-agent`, `@earendil-works/pi-tui`. Runtime: Node.js ≥20, optional `rtk` binary.
- Windows-specific fixups applied automatically (`cd /d` path normalization, `PYTHONIOENCODING=utf-8` prepend for Python commands).
- Related extensions from the same author: `pi-tool-display` (diff visualization), `pi-permission-system` (tool/command permission enforcement), `pi-smart-voice-notify` (TTS notifications), `pi-image-tools`.

---

## 5. Harness context (background, from explainx.ai guide)

Useful mental model for where Pi sits relative to a full agent harness. Six components every serious agent system implements:

1. Task definition — what success looks like
2. Context / memory manager — what the model sees each turn
3. Tool execution layer — files, shell, APIs
4. Loop controller — when to call the model again
5. Verification layer — when the task is actually done
6. Failure handler — exits, escalation, partial results

**Pi gives you steps 3–6 as infrastructure on day one.** You still have to supply steps 1–2 (task definition + verification) yourself — the extensions above (especially `pi-observational-memory`) strengthen step 2, but don't replace the need for you to define what "done" looks like for a given task.

- **`AGENTS.md`** — project instructions loaded at startup from `~/.pi/agent`, parent directories, and cwd. Same pattern as Claude Code's project memory / the community `AGENTS.md` standard.
- **`SYSTEM.md`** — replaces or appends to Pi's default system prompt *per project*. Harness-level prompt control without forking the binary.

---

## 6. End-to-end example scenario (multi-day feature build)

**Day 1 — orientation**
```
> Map this repo and find everything related to checkout/payment.
```
`pi-codemapper`'s `map` → `search({query:"checkout|payment|charge"})` gives structure without full reads. `pi-observational-memory` starts silently recording observations as early decisions get made.

**Mid-build — sanity check before a risky change**
```
> Before I refactor processPayment, use expand to show me what depends on it,
> then ask the advisor whether this abstraction is the right call.
```
`expand({symbol:"processPayment"})` gives exact callers/callees/tests; the `advisor` subagent gives a structural opinion from a clean context.

**Long session, noisy output**
`pi-rtk-optimizer` compacts test/build/git output automatically in the background. Check `/rtk stats` occasionally.

**Approaching compaction**
`pi-observational-memory` has been distilling reflections in the background, so compaction is a fast render. Check `/om:status` if curious about pool pressure beforehand.

**Before merging**
```
> Have the reviewer look at the diff for security and code quality before I open the PR.
```
Clean-context `reviewer` subagent, unbiased by having "written" the code.

**Days later, resuming**
```
> /om:view full
```
Reloads full decision history — no re-explaining, no re-litigating settled calls.

---

## 7. Quick-reference: all settings files at a glance

| Extension | Settings location | Namespace |
|---|---|---|
| `pi-observational-memory` | `~/.pi/agent/settings.json` or `.pi/settings.json` | `observational-memory` |
| `pi-minimal-subagent` | `~/.pi/agent/settings.json` or `.pi/settings.json` | `pi-minimal-subagent` |
| `pi-codemapper` | env var only (`CODEMAPPER_BIN`) | — |
| `pi-rtk-optimizer` | `~/.pi/agent/extensions/pi-rtk-optimizer/config.json` (or `$PI_CODING_AGENT_DIR/...`) | top-level JSON |

Project settings (`.pi/settings.json`) override global settings for the extensions that support project scope.
