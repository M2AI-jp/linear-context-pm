---
name: linear-context-pm
description: "Design or audit Linear-centered PM context for AI/Codex work: source inputs, decisions, accepted outputs, atomic delegation, E2E acceptance, test review, and stale-context cleanup. Use for reusable governance or project onboarding; not ordinary one-off Linear data entry."
metadata:
  version: "0.3.7"
---

# Linear Context PM

Keep the project input `X` clean so AI/Codex work converges on the customer outcome in the user's original words:

```text
Y = F(X)
current X -> smallest justified action -> Y -> independent acceptance -> accepted Y only -> next X
```

`X` includes the relevant user originals, SSoT, decisions, repository/code/tests, and authorized Linear or external context. Linear externalizes PM context: goals, decisions, plans, approvals, owners, stale or blocked state, and evidence references. It must not duplicate raw Git, CI, repository, browser, account, or external-service logs; those systems remain authoritative for their own state.

## Scope and authority

- Apply this skill to designing, onboarding, simulating, or auditing a Linear-centered context system.
- Do not apply it to an ordinary one-time request to create, edit, or triage Linear items.
- Design, explanation, simulation, and audit do not authorize writes. Mutate Linear, a repository, a browser, or another system only within the user's explicit authority.
- Apply only the controls, roles, records, reviews, tests, issues, PRs, artifacts, and evidence references required by the next authorized action and the actual customer or implementation claim. For answer-only, audit, discovery, or no-implementation work, do not create Linear records, issues, PRs, tests, reviewers, artifacts, or external side effects unless explicitly authorized or needed for that action.

## Execution loop

Use initiate, plan, execute, monitor/control, and close as PM verbs, not as required document names or response headings.

1. **Read current `X`.** Read the user's original wording and the full user-origin thread that produced the current request before acting. When source history is mixed, declare the active work frame by explicitly separating the current request and outcome, past examples or failures, non-goals, authority boundary, and current versus historical evidence; omit absent categories and do not force headings for simple cases. Attribute each constraint to its source without softening it into vague attribution. Past project outcomes constrain design only as evidence or prohibited effects unless the user explicitly reopens them as current. Then read the current SSoT, active decisions, repository/code/tests, and authorized Linear or external state needed for the next action. Recency alone is not authority. Keep confirmed facts, proposals, unknowns, authority, prohibited effects, and stop conditions distinct; inference is not confirmation.
2. **Fix the outcome from evidence.** After the necessary read-only discovery, state the customer outcome, non-goals, scope, and authority. If the outcome, authority, target, or prohibited effect remains ambiguous and would change the next action, stop and ask one focused question; otherwise continue safe discovery without inventing requirements. Reuse confirmed facts unless a concrete contradiction or named irreversible risk reopens them. Output only blockers that affect the next authorized action or the customer outcome.
3. **Define acceptance before implementation.** Express the smallest useful E2E happy, failure, and regression paths in customer language, including prohibited side effects. A reviewer independent of the implementation qualitatively checks that the tests could falsify the claimed outcome and do not reward proxy metrics. Accepted tests and scenarios become durable context for future work and stale only when affected by a changed decision. When human-only verification is impractical, project setup should define automated or simulated coverage and reserve human verification for final acceptance.
4. **Plan only the next smallest change.** Minimize code, files, dependencies, cost, and coordination. Do not create future-complete backlogs, placeholder modules, or speculative architecture. For repository implementation governed in Linear, one Linear issue changes one file and must define that file's single responsibility, inputs, outputs, dependencies or interfaces, and acceptance; a generic "follow SOLID" instruction is not sufficient. One module PR groups those file-level issues with lint, tests, independent qualitative test review, and independent implementation QA. Repository SSoT, stack/framework/linter choices, root or module AGENTS instructions, module boundaries, and test layout are project setup; when that setup is part of the request, fix it before implementation. For non-code, one change has one purpose and one atomic target.
5. **Delegate one bounded target.** Give the worker all authority the PM has and the worker needs inside that target, and none outside it. The worker resolves in-boundary details autonomously and reports completion evidence or one consolidated blocker at the predeclared stop condition. Fail closed only immediately before the affected action and only for that scope; continue safe, unrelated authorized work.
6. **Accept or reject `Y`.** Require evidence of the declared customer outcome and prohibited effects. Links, counts, passing commands, and agent assertions may support evidence but do not prove the outcome. Promote only independently accepted `Y` into active `X`.
7. **Clean the next `X`.** When the user or SSoT explicitly abandons or replaces code, issues, integrations, or scope, do not retrofit old issues into the new shape; remove obsolete material from active context and preserve only the decision and evidence history still needed. When a decision changes, supersede it, mark only affected dependencies stale, and remove obsolete material from active context while preserving the history needed to explain decisions and evidence.

Every control, review, evidence reference, stop, or retry must name the concrete failure or acceptance decision that requires it. Do not add checks, artifacts, agents, or communication merely for formal completeness.

## Linear use

- Inspect the authorized Linear workspace before relying on any entity, field, relation, workflow, or permission.
- Use the smallest confirmed native Linear primitive that can hold the needed PM meaning. Several meanings may share one native type when that is simpler.
- Store only what cannot be reconstructed from the authoritative source: the decision or unknown, outcome impact, owner or decider, affected scope, resolution or acceptance evidence, and state.
- Reuse Linear's native ID, timestamp, assignee, and state history instead of copying them into record bodies.
- Before an authorized side effect, inspect the actual target state and authority. If a concrete conflict affects the action, use only the smallest evidence-backed stop or recovery needed.

## Required references

- Read [references/framework.md](references/framework.md) completely when designing or auditing the system or onboarding a project.
- Read [references/forward-testing.md](references/forward-testing.md) completely only when independently testing this skill or revising it from an observed result. Do not give that reference to the fresh executor.

## Output contract

Report only what the current decision or next authorized action needs: the outcome and authority boundary, `X` sources used, actual blockers or stale impact, the next action, and the scoped stop. When source history is mixed, include the active-work separation above; for simple cases, this can be one compact sentence rather than separate headings. In substantive updates, state what is being done, why it advances the current outcome, and the next stop or acceptance point; do not turn this into routine status chatter. Make subjects, predicates, dependencies, and input-process-output flows explicit for the user, PM, worker, reviewer, Linear, repository, and external systems that are in scope. Do not present a proposed Linear structure as existing state or management volume as delivered value.
