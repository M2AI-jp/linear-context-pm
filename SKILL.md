---
name: linear-context-pm
description: Design or audit AI/Codex development governance that uses Linear to externalize PM context, decisions, state, evidence references, and stale-context cleanup. Use for reusable governance or project onboarding; do not use for ordinary one-off Linear data entry.
metadata:
  version: "0.5.7"
---

# Linear Context PM

Use this skill to prevent AI/Codex work from drifting away from the user/customer outcome through stale context, overimplementation, proxy metrics, existing-code bias, or unverified completion.

Linear is the PM control plane for this purpose. It is a means to externalize goals, decisions, authority, state, blockers, and evidence references; it is not the product goal, code source of truth, raw log store, or progress proxy.

Keep the project-specific input context `X` clean across AI/Codex sessions:

```text
unknown X0 -> investigated and governed X1 -> model output Y
           -> independent verification -> accepted Y only -> next X
```

The repository and external-system state are parts of `X`; Linear is not a replacement for either. Git and CI retain code changes and raw development logs. Linear retains goals, unknowns, decisions, state, evidence references, approval, and the reasoning that cannot be reconstructed from Git.

For this skill, `X` has two layers:

- **Project memory:** Linear and SSoT records that preserve accepted scope, decisions, inactive future decomposition, evidence references, and stale markers.
- **Active execution context:** the minimal current Context Manifest passed into the next worker/session.

Clean `X` requires both layers: do not inject inactive future work into the active execution context, and do not hide accepted scope by omitting it from Linear.

## Priority hierarchy

1. Keep `X` clean enough for the next Codex session to act from the current truth: complete enough in project memory, minimal enough in active execution context.
2. Use Linear to externalize the procedures and state transitions that protect that cleanliness.
3. Use SSoT, E2E-first acceptance, atomic decomposition, Git-state linkage, independent test review, implementation QA, stale cleanup, and bounded worker authority only as mechanisms for that purpose.
4. Reject any metric or artifact--Issue count, test count, SHA, passing command, link, self-review, or management volume--when it becomes a substitute for clean `X` and accepted user/customer outcome.

## Scope and authority

- Apply this skill to designing, onboarding, simulating, or auditing this governance system.
- Do not apply it to an ordinary one-time request to create, edit, or triage Linear items.
- A request to design, simulate, explain, or audit does not authorize writes to Linear, repositories, browsers, SaaS products, or production systems.
- Mutate Linear or an external system only when the user explicitly authorizes that mutation and its scope.
- Treat project examples as Project Profiles, not universal rules. Never universalize a provider, language, repository layout, data store, or interaction mode from one example.
- Linear work is scoped to an explicit Project Boundary. Do not read, search, list, compare, cancel, archive, copy, or summarize Projects, Issues, Documents, or milestones outside that boundary.
- For a new Linear Project, use the user/SSoT-specified or current/default Linear team as the destination; never read existing Projects. The returned Project ID becomes the boundary.
- If work on an existing Project is required, the user or current SSoT must provide the exact Project ID or URL before any Project read. A name search, similar title, archived state, canceled state, or unfinished Issue is not authority.

## Declare context before proceeding

At the start of each material stage and after any change of direction, state concisely:

1. **Confirmed:** user-confirmed facts and authoritative evidence.
2. **Proposed:** current recommendations that remain changeable.
3. **Unknown:** unresolved facts that can change the plan.
4. **Authority:** permitted reads, writes, external effects, and approvers.
5. **Stop conditions:** missing or contradictory inputs that prohibit the next stage.

Do not silently convert an inference, generated output, test result, or summary into a confirmed fact.

## Operating method

Follow the hierarchy above when these steps conflict; lower-level mechanisms never override clean `X` and the accepted user/customer outcome.

Read the steps as a dependency order: define the context boundary, make Linear hold the state and decomposition, then execute bounded work and admit or reject outputs into the next `X`.

1. Separate the invariant **Common Kernel** from the target-specific **Project Profile**.
2. Start with `G0A` (provisional purpose, investigation authority, prohibited actions), perform the read-only `G1` Context Inventory, then establish `G0B` (final goal, scope, authority). This avoids requiring final scope before discovery.
3. Establish the Linear Project Boundary before any Project-level read or write. For a new Project, use the user/SSoT-specified or current/default Linear team and do not read existing Projects; for an existing Project, use only the exact user/SSoT-provided Project ID or URL.
4. Separate Linear decomposition from execution. Before any Linear planning write, draft a coverage ledger for user-accepted scope: scope item, classification (`current execution`, `inactive planned`, `unknown`, or `excluded`), representing Linear object, consumer or acceptance path, and omitted reason. If an accepted item is represented only by a checkpoint title, postponed because execution is not yet authorized, or omitted without proof that it is duplicate, invalid, stale, or out of scope, stop before mutation. Unknown or unaccepted items receive Context Issues, not implementation Issues. Minimize code, files, dependencies, cost, simultaneous work, and active execution context, not useful Linear issue count.
5. Establish contracts, SSoT, a task-specific Context Manifest, Context Lint, customer-language E2E, independent qualitative test review, and atomic implementation planning in that order.
6. In a code Project Profile, enforce these invariants together: the root `AGENTS.md` points to the current SSoT and Context Manifest; approved Decisions fix the stack, framework, exact versions, and linter before implementation; folders are loosely coupled modules with module `AGENTS.md`; each file-changing Issue changes one file; Git-state Issues separately govern branch, PR, review handoff, merge, main promotion, rollback, or reconciliation; each module PR includes lint, tests, independent review of the tests, and independent implementation QA.
7. In a non-code Project Profile, map an Atomic Change Issue to one reversible operation purpose, one configuration target, one document responsibility, or another explicitly bounded unit.
8. At execution time, give the worker one complete boundary: purpose, target, SSoT inputs, all read/write/tool/effect authority already held by the PM and required inside that boundary, prohibited effects, acceptance criteria, and stop conditions. The worker acts autonomously inside that boundary and does not ask for stepwise approval unless a stop condition is reached.
9. Promote an output into project memory or active execution context only after its predeclared evidence and independent approval pass. Otherwise retain it as proposed, rejected, failed, or unknown.
10. Supersede decisions; never rewrite their history. Propagate staleness through SSoT, manifests, E2E, tests, changes, evidence, deployed state, and external side effects.
11. Run Context Lint continuously as detection. Treat any cleanup rewrite as its own atomic change with regression evidence and independent review.
12. Close by removing obsolete material from current SSoT/Manifest and active execution context, archiving only needed history, reconciling external state, and emitting the next minimal Context Manifest.

Fail closed when required authority, SSoT, evidence, ownership, or consistency is missing. A link, commit, passing command, issue count, test count, or agent assertion is not by itself proof of customer outcome.

## Required references

- Read [references/framework.md](references/framework.md) completely when designing or auditing a Linear structure, gate model, SSoT system, Context Lint, E2E/test workflow, or project simulation.
- The test coordinator and post-run evaluator read [references/forward-testing.md](references/forward-testing.md) completely when independently testing this skill or revising it from observed results. Never give that reference, prior findings, expected answers, or proposed fixes to the fresh executor.

## Output contract

For a design or simulation, report:

- the current context declaration and authorization boundary;
- the Common Kernel separately from the Project Profile;
- the Linear Project Boundary, including whether it is a newly returned Project ID or an exact user/SSoT-provided existing Project ID or URL;
- gates with inputs, outputs, owner, approver, exit criteria, and stop conditions;
- the pre-write coverage ledger for accepted scope, blocking Context Issues, the fine-grained inactive decomposition, and the single current execution checkpoint;
- the evidence and stale-propagation rules;
- what is deliberately not created yet;
- the next authorized action, or the exact reason work must stop.

Do not present proposed Linear structure as if it already exists. Do not use management volume, formal completeness, or successful self-review as a proxy for delivered value.
