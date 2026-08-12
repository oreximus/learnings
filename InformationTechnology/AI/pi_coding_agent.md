# Pi Coding Agent Setup Notes

**Date: 2026-08-13**

**Sources**:
1. https://www.reddit.com/r/PiCodingAgent/comments/1t41thp/my_powerful_pi_agent_setup/
2. https://explainx.ai/blog/pi-minimal-agent-harness-mario-zechner-guide-2026
3. https://claude.ai/share/c4ac2b83-3183-4719-b9a6-b90df1e5cc8a
4. https://github.com/elpapi42/pi-observational-memory/blob/master/README.md

## Notes from the source #1:

- [pi-fork](https://github.com/elpapi42/pi-fork): a basic and minimalist subagents extension.
**This brings a single thing to the table**. great context
management, the main agent context will only contain relevant
information, the main agent context will be richer and denser per
token, all the noise stays out of the main agent context.

- [pi-observational-memory](https://github.com/elpapi42/pi-observational-memory): is a custom compaction algorithm inspired/copied from
[Mastra's article](https://mastra.ai/blog/observational-memory). This custom compaction alogrithm enables pi sessions to last
forever without maxing out the context window and keep the agent focused.
    - This combined with the rich context window of the pi-fork extension creates a rich
    re-callable memory system that stays relevant no matter how many weeks you have been
    using the same session nor the compactions it have withstand.
    - Useful commands, once it's running: **FROM SOURCE #3 AND #4**:
        - `Memory counts, drift, pool pressure, worker state, last errors`:
        ```
        /om:status
        ```
        - Shows + copies current visible memory
        ```
        om:view
        ```
        - Full memory state (visible memory can be empty before the first V3 compaction
        -- use this to check what's actually recorded)
        ```
        om:view full
        ```
        - Pulls original source evidence for a specific observation/reflection id
        ```
        recall <id>
        ```
        
        > One important note: you're mid-upgrade territory
        - **V3 rewrite** that is not backward-compatible with 
        V2. If you (or a prior config) used V2 settings, they'll be silently ignored
        (V3 falls back to defaults, not an error) - so check your settings against the
        migration table in the doc (e.g. `observationThresholdTokens` -> `observeAfterTokens`,
        -> `compactionModel` -> `model`, etc.), and start a fresh Pi session after upgrading,
        since existing sessions may still be showing old V2-era compaction text until a new V3
        compaction runs.

- [pi-minimal-subagent](https://github.com/elpapi42/pi-minimal-subagent): we use this to enable 2 subagents: the ***"advisor"*** (concept copied from claude
code) and the ***"reviewer"***.
    - The fork from pi-fork are extensions of the main agents, they are basically the same 
    agent, they share the same context.
    - These two agents give access to the main agent to different point of view less biases, 
    with clean context windows. The reviewer takes care of code quality, security and ux 
    of the changes introduced by the main agent. The advisor is for strategical decisions 
    around architecture and product.

- [pi-codemapper](https://github.com/elpapi42/pi-codemapper): a wrapper of [codemapper](https://github.com/p1rallels/codemapper) that enables efficient codebase exploration.
This codemapper repo is really bad and unmaintained, it had a cache bug I had to patch
myself. I'm looking forward to switching to [cymbal](https://github.com/1broseidon/cymbal) when I get some free time.

- [pi-rtk-optimizer](https://github.com/MasuRii/pi-rtk-optimizer): This is a classic, not much to say here, it saves some tokens.

> Overall this is the personal agent setup never forgets and can be useful for weeks
before the context window gets maxed out.

## Notes from the source #2:

### Pi in harness terms

- Our `agent harness guide` defines six components every serious agent system
implements:
    1. `Task definition` - what success looks like.
    2. `Context / memory manager` - what the model sees each turn.
    3. `Tool execution layer` - files, shell, APIs
    4. `Loop controller` - when to call the model again
    5. `Verification layer` - when the task is actually done
    6. `Failure handler` - exits, escalation, partial results


- Mapping Pi to your first custom harness:
    - Agent harness guide sequence is: `define success` -> `write verification` -> `simplest`
    `loop` -> `hard exit` -> `context` -> `failures` -> `instrument` -> Pi gives you steps 3-6 as
    infrastructure on day one. You still supply **step 1-2** (***task + verification***).

### AGENTS.md and SYSTEM.md

- `AGENTS.md` - project instructions loaded at startup from `~/.pi/agent`, parent
directories, and the current working directory. Same pattrern as Claude Code's
project memory and the community `AGENTS.md` standard discussed in
`memory.md persistence`.

- `SYSTEM.md` - replace or append to PI's default system prompt `per project`. This
is harness-level prompt control without forking the binary.
