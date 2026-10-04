# Codex 10x: build, verify, reuse

2026-10-04 · All **9 tabs** in Chrome’s “Codex 10x” group reviewed; **3 full video transcripts** read. Deduplicated, paraphrased extraction. Rank = likely usefulness for Databricks SA delivery, reusable assets, and multiple projects—not measured speedup.

## Do these first, in order

| # | Action | Concrete result / completion check | Sources |
|---|---|---|---|
| 1 | Give every task an outcome contract: **goal, context, constraints, done when**. | One customer problem → one artifact → named checks. Measure time to accepted output, correction rounds, review minutes, and reuse—not agent/commit count. | [1], [4], [6] |
| 2 | Make Codex **see and verify its work**. | Setup/build/check commands work; relevant tests pass; actual UI/data behavior is observed; diff reviewed; evidence saved. For demos: sample data, expected results, failure handling. | [1], [3], [6] |
| 3 | Finish one reusable SA asset before starting another. | A working demo, architecture decision, troubleshooting playbook, or customer-ready explanation; turn recurring successes into a narrow skill. | [1], [6] |
| 4 | Keep `AGENTS.md` short and executable. | Repo map, run/test commands, conventions, boundaries, verification. Use global → repo → directory guidance; edit generated scaffolds; add rules after repeated mistakes. | [1], [3] |
| 5 | Use one chat per coherent outcome; save a handoff. | Decision, files, evidence, blocker, next action. Resume the same problem; fork only when it branches. | [1], [3] |
| 6 | Plan or interview before ambiguous builds. | Resolve assumptions, dependencies, acceptance checks; use `/plan` or a durable execution plan. Scale gates/tests to actual risk. | [1], [3], [4] |
| 7 | Use `/goal` for a bounded milestone. | Objective + observable checks + permitted scope + blocker/stop rule; steer while running; pause/resume or revise the goal when needed. | [4] |
| 8 | Isolate concurrent writers. | Separate worktrees/branches; explicit file ownership; set up dependencies, ports, test data/DBs, and environment per checkout; integrate and recheck. | [1], [7], [8] |
| 9 | Explicitly delegate independent, mostly read-only work. | Code explorer + docs verifier + reviewer return short findings with file/source references. One coordinator integrates; begin with at most two workers and increase only if review stays timely. | [2], [7] |
| 10 | Connect only tools that remove a real manual loop. | Official docs MCP for current APIs; browser tools for UI evidence; CLI for deterministic local operations. Reuse existing skills/tools before adding orchestration. | [1], [2], [3] |
| 11 | Review intent and architecture, not merely generated lines. | Ask what problem the change solves, whether it fixes the root cause, and whether the same defect affects other paths. Small focused changes; give contributors credit. | [3], [6] |
| 12 | Automate only a workflow that already works manually. | Skill = method; schedule = cadence. For this workflow, first record three useful manual runs, then approve exact prompt/cadence/write scope/stop rule. | [1] + operating preference |

**First experiment:** one locally working Databricks-oriented demo with sample data, documented checks, a two-minute explanation, and a reusable troubleshooting note. Record baseline versus assisted time. Verify tool/auth availability; authorize workspace calls/deployment separately.

## One prompt to reuse

```text
/goal Finish [one outcome] in [repo].
Context: [files, authoritative docs, example, observed error].
Deliver: [working artifact + brief explanation + evidence].
Done: [observable behavior + relevant checks + reviewed diff].
Boundaries: [allowed files/tools]; local work only unless explicitly authorized.
Work: inspect first; clarify consequential ambiguity; plan if needed;
implement; run relevant checks; inspect actual behavior; fix; summarize.
If useful, use two read-only subagents: docs verification and review.
Return their findings with sources; integrate them into one result.
Stop/escalate: missing access, unresolved requirement, or repeated identical
failure after trying a different approach. Save evidence and one next action.
```

## Complete 50-tip playbook, compressed

All 50 tips from [3], paraphrased below. **A** = apply now; **B** = add when friction proves need; **C** = defer or adapt. These are practitioner suggestions, not universal rules.

| Category (count) | Extracted actions | Priority / adaptation |
|---|---|---|
| Prompting (3) | Demand evidence/diff; reconsider a mediocre fix with new knowledge; provide bug and desired behavior without prescribing every step. | A; preserve useful work before a rewrite. |
| Planning (4) | Explicit plan; phased checks; independent plan review; precise specification. | A; extra reviewer/tests only when warranted. |
| AGENTS (5) | Concise guidance; personal overrides; first-try test setup; consistent completed migrations; enforce deterministic settings through config. | A; 150 lines is a heuristic, byte limits/version matter. |
| Agents (3) | Narrow feature roles with relevant skills; delegate to protect main context; separate implementation/review contexts. | B; explicit delegation and review capacity govern. |
| Skills (7) | Name/description metadata; progressive folders; accumulated gotchas; trigger-oriented description; omit obvious advice; goals/constraints over rigid steps; scaffold and standardize invocation. | A/B; validate on 2–3 representative cases. |
| Hooks (3) | Logging/security/validation; formatting; lighter context on clear versus startup/resume. | B; verify client support and event names before configuring. |
| Memories (2) | Cross-session memory; secret/untrusted-content controls/reset. | B; verify settings; memory is fallible; reset is consequential. |
| Workflows (4) | Simple native workflow for small tasks; permission profiles; conservative approvals; fork/resume. | A; preserve transaction-specific approvals. |
| Advanced (5) | Parallel fan-out; headless `codex exec`; sandbox + approvals; worktrees; architecture diagrams. | B; use the smallest useful workflow. |
| Git/PR (3) | Small focused PRs; squash suggestion; frequent completed-task commits. | A; merge strategy follows repo/team policy. |
| Debugging (5) | Background logs; browser console tools; screenshots; independent model review; direct repo search over a stale index. | A/B; retrieval choice depends on corpus and permissions. |
| Utilities (4) | Terminal/tmux workflow; voice dictation; completion feedback; personalized config. | B/C; choose app/IDE/CLI by task; voice “10x” is unproven. |
| Daily (2) | Update client; read changelog. | B; relevant stable updates beat ritual daily churn. |

**Feature inventory from [3]:** session commands; custom agents; skills/plugins/marketplaces; memories; MCP over STDIO/HTTP with OAuth; layered config/profiles; execution rules; hooks; speed modes; code review; resume/fork/archive. Its weather example composes agent → skill. Superpowers, Spec Kit, gstack, GSD, OMX, Compound Engineering, and cross-model workflows are optional frameworks around research → plan → execute → review → ship; none is required to begin.

## Parallelism: choose the smallest mechanism

| Mechanism | Use / completion evidence | Rank |
|---|---|---|
| Native subagents | Independent exploration/review/triage; short cited findings; coordinator combines results. Separate threads share the workspace. | First |
| Custom agents | Repeated narrow role: required `name`, `description`, `developer_instructions`; optional model/effort/sandbox/MCP. Personal `~/.codex/agents/` or repo `.codex/agents/`. | When repeated |
| Worktrees | Concurrent feature writers; branch/directory isolation; verified integrated result. Isolation does not isolate shared ports, databases, credentials, or remote resources. | Before parallel writes |
| CSV fan-out | Repetitive per-file/service audits; structured row results. Check availability; older articles describe `spawn_agents_on_csv`. | When batch-shaped |
| Headless CLI | Repeated scripted checks: `codex exec --json` for JSONL events; schema-constrained output where supported; captured final report and status. | After manual reliability |
| tmux/orchestrators | Sustained independent sessions needing job IDs, logs, steering, maps; articles discuss codex-orchestrator, codex-yolo, OMX. | Defer; review source/permissions first |
| Symphony / issue dispatch | Durable issue-to-isolated-run control plane; reviewable outputs and recovery. | Last; team-scale complexity |

Start with one coordinator + two workers. More agents increase token/tool work and review burden. Cap backlog; investigate repeated failures; use explicit budgets where supported. Worktrees still need dependency setup and merge tracking; remove them only after preserving work. Firecrawl’s search/scrape MCP is one optional research adapter, not a prerequisite. [2], [7], [8]

## Video takeaways worth acting on

**Goals, 1:38 [4]:** measurable success; plan/interview first; steering; side chats for questions without stopping the main run; pause/resume/edit. Hours or days of activity is not completion evidence.

**Developer updates, 7:12 [5]:** [1:28](https://www.youtube.com/watch?v=eiQgljOrkWU&t=88s) appshots provide screen + app context; [2:11](https://www.youtube.com/watch?v=eiQgljOrkWU&t=131s) browser annotations and inline diff edits tighten feedback; [3:17](https://www.youtube.com/watch?v=eiQgljOrkWU&t=197s) Sites is a hosting option; [3:51](https://www.youtube.com/watch?v=eiQgljOrkWU&t=231s) coordinator tasks/worktrees, priorities, and conversation references organize projects; [4:57](https://www.youtube.com/watch?v=eiQgljOrkWU&t=297s) mobile task/review/SSH workflows; [5:36](https://www.youtube.com/watch?v=eiQgljOrkWU&t=336s) PR context, failed-check fixes, and inline review. The model/Ultra launch and Build Week invitation are historical; verify current availability. Creation/pinning, publishing, and merging remain explicit actions.

**Steinberger, 31:28 [6]:** [6:29](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=389s) recover an unfinished project into a spec, then verify with a browser; [8:02](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=482s) reusable small tools can compose into a product—actual repeated use and user demand are stronger signals than social engagement; [10:45](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=645s) tools enable unexpected problem-solving; [12:58](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=778s) trust/sandbox boundaries matter; [16:12](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=972s) stop the supervisor as well as the process, or it may restart; [18:09](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=1089s) practice, challenge assumptions, ask for questions, and keep the architecture in view; [20:01](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=1201s) avoid optimizing setup instead of delivering; [21:51](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=1311s) judge behavior and system fit, while retaining risk-appropriate review; [24:10](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=1450s) review contributor intent/root cause and credit them; [26:37](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=1597s) hackability and ordinary-user safety conflict; design for foreseeable deployment misuse; [29:14](https://www.youtube.com/watch?v=9jgcT0Fqt7U&t=1754s) build a personally useful thing and learn through reps. Burnout/recovery is part of the origin story. His permissive experiments, no-worktree setup, and unread-code claims are personal anecdotes, not recommended enterprise defaults.

## Correct older advice before copying it

- **Current [2]:** delegation requires a direct request or applicable instructions. July’s “automatic without asking” video demo [5] differs from current guidance.
- **Current [2]:** `agents.max_concurrent_threads_per_session` is the documented concurrency key; `max_threads` remains a legacy alias. Do not assume old six-thread/depth examples or client-specific batch controls apply here.
- **Current [1], [2]:** start with GPT-6.1 Sol if available; GPT-6 Luna for lighter bounded work; select supported effort. Older GPT-5.x/o4-mini choices, speed/credit ratios, release dates, and deprecation claims need a fresh check. Defaults inherit unless explicitly overridden; custom agent files can override resolved settings.
- **Current [1]:** Codex can scaffold `AGENTS.md`; [8]’s “only humans should write it” is too absolute. Human review and useful instructions matter.
- **Current [2]:** subagents inherit parent permissions; narrow read-only roles explicitly. More agent work costs more tokens, but exact linear scaling and “8–10 GB per agent” are not universal facts.
- **Adapt [3], [7], [8]:** no blanket squash policy, automatic approval, public bot exposure, arbitrary install scripts, or factory-scale orchestration. Claims of “10x” or team PR increases do not establish your gain.

## Sources, ranked by usefulness

| Rank / ID | Source | Coverage / qualification |
|---|---|---|
| 1 · [1] | [Official best practices](https://learn.chatgpt.com/guides/best-practices) | Entire guide: prompting, plans, guidance, config, validation, MCP, skills, schedules, chats, mistakes. |
| 2 · [2] | [Official subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents?surface=app) | Entire guide: triggering, context, models, controls, permissions, schema, review/UI-debug examples. |
| 3 · [3] | [50-tip GitHub playbook](https://github.com/shanraisshan/codex-cli-best-practice) | README, all 50 tips, feature/workflow/resource inventory; MIT-licensed; version-sensitive. |
| 4 · [4] | [Run long tasks using goals](https://www.youtube.com/watch?v=rgh0hMYPcd0) | Full transcript + description; OpenAI, May 21, 2026. |
| 5 · [5] | [Codex developer updates](https://www.youtube.com/watch?v=eiQgljOrkWU) | Full transcript + chapters; OpenAI, July 14, 2026. |
| 6 · [6] | [Builders Unscripted: Peter Steinberger](https://www.youtube.com/watch?v=9jgcT0Fqt7U) | Full visible transcript + chapters; OpenAI, February 24, 2026. |
| 7 · [7] | [Firecrawl orchestration](https://www.firecrawl.dev/blog/codex-multi-agent-orchestration) | Entire article; June 8, 2026; useful workflow ladder, vendor framing, dated examples. |
| 8 · [8] | [Vaughan: parallel patterns](https://codex.danielvaughan.com/2026/04/18/running-multiple-codex-agents-parallel-orchestration/) | Entire article; page says updated October 4, 2026; native/tmux/worktrees and resource/coordination tradeoffs. |
| 9 · private tab | Claude conversation: “Codex CLI for multi-product development” | Both messages read; recommendation index, not primary product evidence. Private transcript/link omitted from this public document. |

**Additional leads from the private tab, not independently reviewed:** [Solutions Engineering Partner](https://www.youtube.com/watch?v=_jNbM8pV9oI), [Making AI Tangible](https://www.youtube.com/watch?v=08hgAtg-P_8), [Codex for data science](https://www.youtube.com/watch?v=Lvk_VZOppIY) are most aligned with SA work; then [Steinberger’s longer interview](https://newsletter.pragmaticengineer.com/p/the-creator-of-clawd-i-ship-code), [Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed), and [Just Talk To It summary](https://simonwillison.net/b/9052). Prefer direct sources over recaps/vendor posts; broad beginner courses and social feeds are low priority for this objective.

[1]: https://learn.chatgpt.com/guides/best-practices
[2]: https://learn.chatgpt.com/docs/agent-configuration/subagents?surface=app
[3]: https://github.com/shanraisshan/codex-cli-best-practice
[4]: https://www.youtube.com/watch?v=rgh0hMYPcd0
[5]: https://www.youtube.com/watch?v=eiQgljOrkWU
[6]: https://www.youtube.com/watch?v=9jgcT0Fqt7U
[7]: https://www.firecrawl.dev/blog/codex-multi-agent-orchestration
[8]: https://codex.danielvaughan.com/2026/04/18/running-multiple-codex-agents-parallel-orchestration/
