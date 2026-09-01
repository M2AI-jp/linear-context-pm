# Minimal PM Context

Use this guidance only to make the next justified move toward the customer or user outcome in the user's original words.

## Working model

`Y = F(X)`: the output is a function of the current input. `X` includes the user originals, governed facts with their SSoT (authoritative source and conflict rule), active decisions, repository/code/tests, and authorized Linear or external state. Only independently accepted output enters the next `X`.

Apply only the controls, roles, records, reviews, tests, issues, PRs, artifacts, and acceptance evidence references required by the next authorized action and the actual customer/user or implementation claim. Answer-only, audit, discovery, or no-implementation work does not create Linear records, issues, PRs, tests, reviewers, artifacts, or external side effects unless explicitly authorized or needed.

Read the full user-origin thread relevant to the current request, SSoT, repository, and authorized Linear or external state before requesting new input. Assistant conclusions and generated summaries may locate primary material but do not replace it. When source history is mixed, separate the current request and outcome, past examples or failures, non-goals, authority boundary, and current versus historical evidence; omit absent categories and avoid forced headings for simple cases. Attribute constraints to their source without softening them into vague attribution. Past project outcomes constrain design only as evidence or prohibited effects unless explicitly reopened. Recency alone is not authority. Keep confirmed facts, proposals, unknowns, authority, prohibited effects, and stop conditions distinguishable.

Keep reusable invariants separate from project-specific facts. The reusable invariants are outcome priority, explicit authority and provenance, independent acceptance where required, atomic work, stale marking for changed decisions, minimal work/cost/files/dependencies, and fail-closed behavior scoped to the affected action. Project-specific facts include actors, repositories, tools, versions, commands, identifiers, UI sequences, risks, acceptance context, and recovery choices.

## Minimal lifecycle

These are logical checks, not required meetings, files, Linear records, or response sections. One source or observation may satisfy several checks; combine them whenever doing so preserves the customer/user outcome and authority boundary.

| PMBOK phase | Minimum check and output |
|---|---|
| **Initiate** | From the user originals, identify the provisional outcome, read authority, and prohibited effects; inspect only missing primary state; then fix the outcome, non-goals, scope, and execution authority. If outcome, authority, target, or prohibited effect remains ambiguous and would change the next action, ask one focused question; otherwise continue safe discovery without inventing requirements. Reuse confirmed facts unless a concrete contradiction or named irreversible risk reopens them. Output only actual blockers, not a speculative implementation backlog. |
| **Plan - acceptance** | Before implementation, define the smallest useful customer/user-language E2E happy, failure, and regression paths with prohibited side effects. The tests must fail when the claimed experience is false; their existence, count, or internal coverage is not acceptance. An implementation-independent reviewer checks falsifiability and proxy-metric risk. Accepted tests and scenarios become durable context and stale only when affected by a changed decision; when human-only verification is impractical, project setup defines automated or simulated coverage and reserves human verification for final acceptance. |
| **Plan — next atomic change** | Define the next smallest complete checkpoint. Do not create a future-complete backlog outside it, and do not omit required atomic issues inside it. The checkpoint contract determines issue count; issue count is not itself a minimization target. Replacement of stale work removes obsolete material from active `X`; it does not collapse the checkpoint below its required file targets and Git-state transitions. A checkpoint is valid only when it has accepted input, process, output, dependencies, downstream consumers, acceptance observation, promotion rule, and state transition contract; a title or phase label is not a checkpoint. |
| **Execute and monitor/control** | The worker acts autonomously inside the delegated boundary. Code work is checked at the module PR with lint, tests, independent test review, and independent implementation QA; non-code work uses the smallest equivalent review justified by its risk and acceptance. |
| **Accept and close** | An authorized acceptor observes the declared outcome and prohibited effects. Promote accepted output only, handle affected external state from authoritative evidence, stale affected dependencies, and remove obsolete active context before forming the next `X`. |

If information is missing, fail closed immediately before the action it affects and state the resumption condition. Continue safe discovery and unrelated authorized work.

## Minimal Linear realization

Inspect the authorized Linear workspace before relying on any entity, field, relation, workflow, or permission. Use the smallest confirmed native primitive that can hold the needed PM meaning; several meanings may share one native type when that is simpler.

Use Linear according to its [official concept model](https://linear.app/docs/conceptual-model), not as a generic PM database: issues track individual pieces of work, teams own workflows, cycles plan near-term work, projects group issues around shared outcomes or deliverables, initiatives connect related projects around broader goals, and views organize navigation without changing the work itself. For agent work, follow Linear's [AI Agents](https://linear.app/docs/agents-in-linear) model: delegation to an agent does not remove human ownership. For stale legacy work, follow Linear's [import guidance](https://linear.app/docs/import-issues): activate only what is still needed, and prefer a clean break when history would add clutter.

Store only the minimum PM context that cannot be reconstructed from Git, CI, the repository, or external systems. Record the reason a decision, unknown, owner, accepted output, blocked state, stale state, or evidence reference matters to the next action or customer/user outcome. Reuse Linear's native ID, timestamp, assignee, and state history instead of copying them into record bodies. Use durable approval or checkpoint material only when the user's actual workflow explicitly requires it.

## SSoT, active context, and staleness

- For each governed fact, SSoT means its authoritative source and conflict rule; it does not require copying facts into one central document. For code, Git/PR state is authoritative for changed files and execution artifacts; Linear is authoritative only for PM decisions, owners, acceptance/stale state, and evidence references. Connect them by reference without duplicating raw logs.
- For repository work, define the Git/Linear transition contract before execution. Each Linear state needs an entry condition, exit condition, authorized mover, and relation to branch, PR, review, merge, main promotion, rollback, or reconciliation. Git state may trigger review or reconciliation, but it does not by itself prove Done.
- Keep active context to the goal, active decisions, target inputs, authority, and blockers for the next action.
- Check active context at meaningful boundaries such as session start, a decision change, and immediately before acceptance or promotion. Detect missing provenance, conflict, stale dependency, unauthorized state, and obsolete active context; do not require continuous rewriting or treat a clean check as customer acceptance.
- When the user or SSoT explicitly abandons or replaces code, issues, integrations, or scope, do not retrofit old issues into the replacement. Remove obsolete material from active `X` and retain only needed decision and evidence history.
- When a decision changes, supersede rather than overwrite it. Mark affected plans, E2E/tests, artifacts, evidence, deployed state, or external effects stale or blocked, and reopen only the smallest affected work. Remove obsolete material from active `X` while retaining necessary decision and evidence history.

## Code and non-code work

- For repository implementation governed in Linear, file issues and Git-state issues are separate and additive. Create every required atomic issue inside the current checkpoint: a file issue governs exactly one file target and names that file's single responsibility, inputs, process, outputs, dependencies or interfaces, downstream consumer, and acceptance; "follow SOLID" alone is not enough. A Git-state issue governs exactly one shared repository transition such as branch/PR creation, review handoff, merge, main promotion, rollback, or reconciliation; do not create Linear issues for local git commands or raw logs. One module PR groups the complete set of file issues and required Git-state issues with lint, tests, independent qualitative review of the tests, independent implementation QA, and references between Linear records and Git/PR state.
- Repository SSoT, stack/framework/linter choices, root or module AGENTS instructions, module boundaries, and test layout are project setup. Fix them before implementation only when setup is part of the request.
- For non-code work, one atomic change has one purpose and one target.

## Live work and side effects

Before an authorized side effect, inspect the actual target state and authority. If a concrete conflict affects the action, use only the smallest evidence-backed stop or recovery needed. Never assume recovery from an export, log, code path, or other unrelated artifact.

Use a control, reviewer, evidence item, or retry only when it is required by a named failure or acceptance decision. Do not add them merely for safety. Preserve the required code module-PR lint, tests, independent test review, and independent implementation QA; outside that invariant, choose the smallest control proportional to the actual effect.

An atomic change delegates all authority the PM holds and the worker needs for one target in a single grant. It does not grant authority outside that target. The worker resolves authorized local unknowns without stepwise approval or routine status exchange; an unresolved condition blocks only when its predeclared stop condition is reached, and is returned as one consolidated blocker.

Substantive updates state what is being done, why it advances the current outcome, and the next stop or acceptance point. Do not create routine status chatter as a proxy for progress.
