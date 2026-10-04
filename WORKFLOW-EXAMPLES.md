# Complete workflow examples

Copy one into the relevant project chat. Each prompt covers an action from [CODEX-10X.md](CODEX-10X.md), with concrete scope, output and completion proof. Retail scenarios are fictional; existing project state must be inspected live.

Demo sequence: **1 → 7 → 2 → 11 → 3**. Use the other prompts when their action is needed.

| Reusable workflow | Examples |
|---|---|
| Finish one verified outcome | 1, 2, 7, 8, 9, 11 |
| Turn evidence into a decision | 6, 11 |
| Reconcile and resume | 5, 12 |
| Sources to reusable asset | 3, 4, 10 |
| Learn, apply and explain | 3 |

## 1. Define the outcome contract

**Slug:** `plan-demo` — Writes the demo's scope, seed case, and acceptance checks in PLAN.md before implementation.

```text
In this LangGraph project, inspect instructions, the newest handoff and existing code. Write PLAN.md for the smallest local retail-support agent: START -> support -> END, deterministic response, synthetic ticket only. Seed case: "My item arrived damaged" returns "Escalate to human support." Define permitted files, dependencies, state input/output, one meaningful test and failure handling. Done means executable verification commands and observable acceptance criteria are documented. Preserve existing work; ask only about consequential unknowns. Stop after the plan; no workspace calls, deployment or spend.
```

## 2. Make the result observable

**Slug:** `verify-demo` — Runs the demo and relevant checks, fixes local failures, and saves expected versus actual results.

```text
Verify the local retail-support agent against PLAN.md. Inspect its environment and actual run commands; run the documented seed case and the relevant tests. Show initial state, the support-node update, execution path and final response. Check malformed input handling. Fix failures within this demo's local files and rerun affected checks. Save commands, expected versus actual output and limitations in VERIFICATION.md. Done means behavior matches the plan; label unavailable checks explicitly. No live model calls or deployment.
```

## 3. Finish one reusable field asset

**Slug:** `build-field-guide` — Turns a verified demo and an explanation practice rep into a reusable SA field guide.

```text
Use the verified local LangGraph demo to prepare a reusable SA explanation. Ask me for a 60-second explanation of state, node, edge and why deterministic mode helps validation; wait for my attempt. Correct one gap, let me retry, then ask a fresh customer objection. Save FIELD-GUIDE.md: setup, synthetic example, expected output, a two-minute customer talk track and evidence-backed troubleshooting. Mark covered versus demonstrated skills; judge vocal delivery only from audio. Done means the guide reproduces verified behavior and records my actual practice evidence. Keep it local.
```

## 4. Make AGENTS.md executable

**Slug:** `write-repo-guidance` — Records verified setup, run/test commands, conventions, and boundaries in the repo's AGENTS.md.

```text
Inspect this demo's applicable parent instructions, repo layout and verified commands. Update only the repo-level AGENTS.md with a concise map, environment/setup commands, run/test commands, conventions, verification expectations and local-only boundaries. Preserve existing policies and human edits. Include only commands actually checked; label missing dependencies. Read the result back and review the diff. Done means another run can locate, execute and verify the demo without guessing. Do not change global guidance, permissions or unrelated files.
```

## 5. Save a handoff and resume correctly

**Slug:** `save-project-handoff` — Reconciles current evidence, advances an authorized step, and records the next action for resumption.

```text
Reconcile this project's newest handoff with current files, checks and receipts. Separate completed, remaining, blocked and unverified work; preserve completed outputs. Complete one authorized local next step if its scope is already clear. Save the handoff using the project's existing convention, or HANDOFF.md if none exists: decisions, changed files, evidence, blocker, one next action and stop condition. Follow the Personal OS session template where applicable. Done means the handoff matches inspected state. Continue in this chat; no new tasks or external writes.
```

## 6. Plan an ambiguous SA build

**Slug:** `prepare-sa-decision` — Creates a concise customer-call brief with architecture options, discovery questions, and a recommended proof exercise.

```text
Prepare CALL-PREP.md, maximum 400 words, for a fictional retail team seeking consistent return-policy answers. Compare deterministic routing with retrieval plus an LLM; assess policy grounding, access controls, human escalation, evaluation and operating effort. Inspect existing project evidence and verify changing technical claims against official docs. Separate facts, assumptions and unknowns. Recommend one starting architecture, five discovery questions, the smallest proof exercise and a 60-second talk track. Done means the next customer decision and validation criteria are explicit. Draft only; no customer messages or cloud changes.
```

## 7. Run a bounded goal

**Slug:** `finish-local-milestone` — Implements the missing local agent pieces and continues until the documented behavior and checks pass.

```text
/goal Finish the smallest local retail-support LangGraph milestone in this project, using existing work and PLAN.md: deterministic START -> support -> END, reproducible environment, one meaningful passing test and recorded actual output. "My item arrived damaged" must return "Escalate to human support." Inspect first, implement only missing pieces, verify behavior and save a short handoff. Done means the documented command reproduces that response and checks pass. Local files only; no hosted calls, workspace mutations or spend. If blocked, report evidence, an attempted alternative and one unblock action; never mark unverified work complete.
```

## 8. Isolate concurrent writers

**Slug:** `isolate-demo-writers` — Separates two workers into worktrees, integrates their changes locally, and verifies the combined result.

```text
In this Git-backed demo, preserve the working tree and create two managed worktrees from current HEAD. Use two worker agents: one owns only synthetic fixtures and their relevant checks; the other owns only the setup/talk-track documentation. Give each its own environment and explicit file ownership; avoid shared ports, writable data and remote resources. Review both results, integrate compatible changes locally and rerun affected checks. Done means the combined result passes and each changed file has a clear owner. Report worktree paths; no pushes or destructive cleanup.
```

## 9. Delegate independent review

**Slug:** `delegate-demo-review` — Coordinates two read-only reviewers and combines code and official-documentation findings into REVIEW.md.

```text
Use exactly two read-only subagents to review this local retail-support demo. One checks code, state transitions and existing verification evidence; the other checks architecture claims against current official LangGraph and Databricks documentation. Each returns at most five findings with file/line or source references, uncertainty and one recommendation. Integrate their results into REVIEW.md, separating defects from optional improvements. Done means conflicting claims are resolved or clearly marked. Workers must not edit files, call hosted models or mutate the workspace; only the coordinator writes the local report.
```

## 10. Use tools that remove a manual loop

**Slug:** `research-governance` — Uses available tools and primary sources to produce a governance recommendation with citations and unknowns.

```text
Research governance for the fictional retail-support assistant using existing docs tools, browser access and local project evidence. Verify tool availability and authentication without exposing credentials. Read primary sources; distinguish supported capabilities from proposed integration. Write GOVERNANCE-BRIEF.md, maximum 500 words: access boundary, policy grounding, evaluation, operational risks, one recommended next proof and citations. Record which manual lookup each tool replaced and any missing access. Done means every material recommendation has evidence or an explicit unknown. No plugin installation, new connections or cloud writes.
```

## 11. Review intent and root cause

**Slug:** `review-root-cause` — Checks changes against customer intent, reproduces defects, and verifies focused local fixes.

```text
Review the demo's current changes against its intended customer outcome and PLAN.md. Identify whether each change solves the underlying problem, preserves interfaces and handles the same failure on other paths. Verify any defect with a concrete reproduction; fix only confirmed defects within the local demo and rerun affected checks. Save a brief intent-to-evidence review with remaining risks. Done means claims match observed behavior and the diff contains no unrelated work. Do not equate a deterministic local test with validated cloud integration. No push or deployment.
```

## 12. Prove the manual loop before scheduling

**Slug:** `prove-manual-loop` — Verifies one studio status run and assesses schedule readiness from three useful manual runs.

```text
In the current video studio, inspect its newest handoff, permissions, manifests, canonical receipts and automation registry. Run its existing read-only status workflow once; save a timestamped report distinguishing historical receipts from freshly observed remote state. Preserve completed batches and duplicates pending review. Count only useful manual runs with evidence. After three, draft a Friday 09:00 America/Phoenix schedule proposal with exact prompt, local write scope, meaningful-change notification rule and stop condition; reconcile existing schedules first. Done means the report and readiness evidence are saved. Do not upload, publish, delete or change schedules without exact approval.
```

Codex capability references: [goals](https://developers.openai.com/cookbook/examples/codex/using_goals_in_codex), [worktrees](https://learn.chatgpt.com/docs/environments/git-worktrees), [subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents). Confirm availability in the client running the prompt.
