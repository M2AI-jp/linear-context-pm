---
name: linear-context-pm
description: Design or audit Linear-centered PM context systems for AI/Codex-driven work, including project discovery, SSoT, evidence, gates, tests, and stale-context removal. Use for reusable development governance or project onboarding; do not use for ordinary one-off Linear data entry.
metadata:
  version: "0.5.1"
---

# Linear Context PM

Use Linear as the PM control plane for keeping the project-specific input context `X` clean across AI/Codex sessions:

```text
unknown X0 -> investigated and governed X1 -> model output Y
           -> independent verification -> accepted Y only -> next X
```

The repository and external-system state are parts of `X`; Linear is not a replacement for either. Git and CI retain code changes and raw development logs. Linear retains goals, unknowns, decisions, state, evidence references, approval, and the reasoning that cannot be reconstructed from Git.

## Scope and authority

- Apply this skill to designing, onboarding, simulating, or auditing this governance system.
- Do not apply it to an ordinary one-time request to create, edit, or triage Linear items.
- A request to design, simulate, explain, or audit does not authorize writes to Linear, repositories, browsers, SaaS products, or production systems.
- Mutate Linear or an external system only when the user explicitly authorizes that mutation and its scope.
- Treat project examples as Project Profiles, not universal rules. Never universalize a provider, language, repository layout, data store, or interaction mode from one example.

## Declare context before proceeding

At the start of each material stage and after any change of direction, state concisely:

1. **Confirmed:** user-confirmed facts and authoritative evidence.
2. **Proposed:** current recommendations that remain changeable.
3. **Unknown:** unresolved facts that can change the plan.
4. **Authority:** permitted reads, writes, external effects, and approvers.
5. **Stop conditions:** missing or contradictory inputs that prohibit the next stage.

Do not silently convert an inference, generated output, test result, or summary into a confirmed fact.

## Operating method

1. Separate the invariant **Common Kernel** from the target-specific **Project Profile**.
2. Start with `G0A` (provisional purpose, investigation authority, prohibited actions), perform the read-only `G1` Context Inventory, then establish `G0B` (final goal, scope, authority). This avoids requiring final scope before discovery.
3. Separate Linear decomposition from execution. Do not invent implementation Issues for unknown or unaccepted scope. When the user authorizes Linear planning for a known accepted scope, decompose that whole scope into the finest justified inactive Issues; keep only the current checkpoint in active `X` and execution authority. Minimize code, files, dependencies, cost, simultaneous work, and active `X`, not useful Linear issue count.
4. Establish contracts, SSoT, a task-specific Context Manifest, Context Lint, customer-language E2E, independent qualitative test review, and atomic implementation planning in that order.
5. In a code Project Profile, enforce these invariants together: the root `AGENTS.md` points to the current SSoT and Context Manifest; approved Decisions fix the stack, framework, exact versions, and linter before implementation; folders are loosely coupled modules with module `AGENTS.md`; each file-changing Issue changes one file; Git-state Issues separately govern branch, PR, review handoff, merge, main promotion, rollback, or reconciliation; each module PR includes lint, tests, independent review of the tests, and independent implementation QA.
6. In a non-code Project Profile, map an Atomic Change Issue to one reversible operation purpose, one configuration target, one document responsibility, or another explicitly bounded unit.
7. At execution time, give the worker one complete boundary: purpose, target, SSoT inputs, all read/write/tool/effect authority already held by the PM and required inside that boundary, prohibited effects, acceptance criteria, and stop conditions. The worker acts autonomously inside that boundary and does not ask for stepwise approval unless a stop condition is reached.
8. Promote an output into active `X` only after its predeclared evidence and independent approval pass. Otherwise retain it as proposed, rejected, failed, or unknown.
9. Supersede decisions; never rewrite their history. Propagate staleness through SSoT, manifests, E2E, tests, changes, evidence, deployed state, and external side effects.
10. Run Context Lint continuously as detection. Treat any cleanup rewrite as its own atomic change with regression evidence and independent review.
11. Close by removing obsolete material from active `X`, archiving only needed history, reconciling external state, and emitting the next minimal Context Manifest.

Fail closed when required authority, SSoT, evidence, ownership, or consistency is missing. A link, commit, passing command, issue count, test count, or agent assertion is not by itself proof of customer outcome.

## Required references

- Read [references/framework.md](references/framework.md) completely when designing or auditing a Linear structure, gate model, SSoT system, Context Lint, E2E/test workflow, or project simulation.
- The test coordinator and post-run evaluator read [references/forward-testing.md](references/forward-testing.md) completely when independently testing this skill or revising it from observed results. Never give that reference, prior findings, expected answers, or proposed fixes to the fresh executor.

## Output contract

For a design or simulation, report:

- the current context declaration and authorization boundary;
- the Common Kernel separately from the Project Profile;
- gates with inputs, outputs, owner, approver, exit criteria, and stop conditions;
- blocking Context Issues and, when Linear planning is authorized for a known scope, the fine-grained inactive decomposition plus the single current execution checkpoint;
- the evidence and stale-propagation rules;
- what is deliberately not created yet;
- the next authorized action, or the exact reason work must stop.

Do not present proposed Linear structure as if it already exists. Do not use management volume, formal completeness, or successful self-review as a proxy for delivered value.
