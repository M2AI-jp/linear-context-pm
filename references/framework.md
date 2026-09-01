# Governance Framework

Use this framework to design or audit a project without turning one project's details into universal policy.

## Kernel and profile

- **Common Kernel:** invariant governance: authority, state semantics, gates, provenance, evidence, independent review, staleness, atomicity, and fail-closed behavior.
- **Project Profile:** confirmed target facts: customer outcome, actors, systems, repositories or documents, environments, owners, risks, commands, acceptance observations, rollback or compensation methods, and local conventions.
- A Profile may instantiate or tighten the Kernel but cannot silently weaken it. Unknown Profile facts remain Context Issues; examples never become Kernel rules.

At every stage declare `Confirmed`, `Proposed`, `Unknown`, `Authority`, and `Stop conditions`. Every gate contract must make these fields explicit: **actor/approver; input; process; output; intended and possible side effects; dependencies; read/write authority; required evidence; stop conditions**. A missing field blocks exit, not necessarily safe read-only discovery.

## Lifecycle and gates

| Gate | Actor, input, process, output, and exit |
|---|---|
| **G0A — provisional initiation** | Sponsor and PM receive the unedited request; record provisional purpose, read/investigation authority, prohibited actions, known systems, and discovery stop conditions. Output is a read-only discovery charter, not final scope. |
| **G1 — Context Inventory** | Authorized investigator reads minimum raw sources and current system state; records provenance, contradictions, unknowns, in-progress work, deployed versions, and external effects. Inspect the target Linear workspace and its authorized interface to confirm which native entity types and operations actually exist, then record the minimal logical-to-native mapping. Output is an evidence-backed inventory plus only blocking Context Issues. No mutation, speculative backlog, or assumed Linear capability. |
| **G0B — final initiation** | Sponsor/approver uses G1 evidence to confirm goal, non-goals, scope, success/failure observations, owners, authority, risk limits, and stop/rollback obligations. Contradiction or missing approver stops planning. |
| **G2 — Project Contracts** | Accountable owners define actor/input/process/output/side-effect/dependency/authority/evidence/stop contracts for each material flow. Output is a consistent Profile contract set; ambiguity that changes behavior remains blocking. |
| **G3 — governed context** | PM assigns each fact to an authoritative SSoT, creates the task's minimal Context Manifest, and runs Context Lint. Output is a provenance-complete active `X`; unresolved conflict, stale dependency, or missing source blocks promotion. |
| **G4 — acceptance design** | Customer representative writes E2E outcomes in customer language. A reviewer independent of implementation qualitatively challenges whether proposed tests can falsify those outcomes, cover prohibited effects, and avoid proxy metrics. No implementation plan exits before approval. |
| **G5 — atomic plan** | PM decomposes only approved next work into reversible Atomic Change Issues with dependencies and evidence. Output is the smallest executable plan; avoid future backlog, cross-purpose units, or invented modules. |
| **G6 — controlled execution** | Authorized worker changes one atomic unit; lint and tests run; an independent reviewer first judges test quality and then QA judges the implementation. A loosely coupled module is the PR checkpoint in code Profiles; use an equivalently bounded review unit in non-code Profiles. Failed evidence stops promotion. |
| **G7 — real acceptance** | Authorized acceptor observes the declared customer outcome and prohibited side effects in the real acceptance context. Synthetic checks, counts, links, commands, or agent assertions may support but cannot replace this evidence. Output is accepted/rejected/failed with an Evidence envelope. |
| **G8 — close and next `X`** | PM reconciles deployed and external state, removes obsolete material from active context without erasing required history, archives evidence, closes or carries explicit unknowns, and emits the next minimal Context Manifest. Inconsistency keeps the gate open. |

This sequence maps to initiate (`G0A/G0B`), plan (`G1–G5`), execute and monitor/control (`G6–G7`), and close (`G8`). Do not skip a gate; repeat the smallest affected gate after change.

## Minimal Linear realization

During G1, verify availability, permissions, fields, state transitions, and stable references through authorized reads of the actual Linear workspace or interface. Map each logical record only after that check. Use the smallest combination of confirmed native entities: a Project may hold the governed outcome; a Milestone may represent a Gate; Issues may represent Context Issues and Atomic Change Issues; a Document may hold the SSoT map, Context Manifest, contracts, or Decision register; Comments may append transitions, decisions, and Evidence envelopes; labels may distinguish record kind or current validity. These are candidate mappings, not assumed capabilities.

Record `logical_type; native_entity_type; native_id; purpose; supported_fields_or_operations; authority; verification_evidence`. If any candidate entity or operation is unavailable or unverified, use another verified primitive or stop with a Context Issue. Never invent a custom field, workflow, immutable history, automation, relation, or permission that G1 did not confirm. Logical semantics remain in the Common Kernel even when several record types share one native primitive.

## Required record schemas

Use stable IDs and timestamps. A record with missing required fields is `incomplete` and cannot authorize downstream work.

**Context Issue**

`id; unknown_or_conflict; outcome_impact; owner; opened_at; source_refs; investigation_authority; required_evidence; dependencies; state; resolution_history; transition_history; resolution_or_stop; updated_at`

States: `open -> investigating -> resolved | blocked | rejected`; reopen `resolved -> open` when its evidence or dependency becomes stale. Append the reopen transition and preserve every prior resolution and its evidence; never rewrite it. Only named evidence resolves the current instance.

**Decision**

`id; question; options_considered; decision; rationale; decider; decision_authority; evidence_refs; affected_nodes; dependencies; decided_at; state; supersedes`

States: `proposed -> approved | rejected`; `approved -> superseded | stale`; never edit an approved decision's substance. A replacement cites `supersedes`, preserves history, and triggers stale propagation.

**Gate**

`id; stage; objective; owner; approver; inputs; process; outputs; side_effects; dependencies; authority; required_evidence; exit_criteria; stop_conditions; state; current_validity; transition_history; decision_refs`

States: `draft -> ready -> active -> passed | failed | blocked`; later invalidation appends `passed -> stale`, and rework may append `stale -> ready -> active`. Reopen the smallest affected gate. Never delete or overwrite the earlier pass: append-only transition history records who changed validity, when, why, and with which evidence, while `current_validity` exposes the latest valid/stale status. Only the approver may pass it.

**Atomic Change Issue**

`id; approved_purpose; bounded_target; owner; independent_reviewers; inputs; process; expected_output; side_effects; dependencies; authority; preconditions; lint_and_tests; acceptance_evidence; rollback_or_compensation; reconciliation; state`

States: `proposed -> ready -> in_progress -> review -> accepted | rejected | failed | rolled_back | compensated`; cancellation records current state and reconciliation. One issue has one reversible purpose and one target responsibility, not necessarily one file.

**Evidence envelope**

`id; claim_or_outcome; acceptance_criteria_ref; raw_artifact_ref; provenance; observed_at; environment_or_context; method; observer; observer_independence; verified_by; verified_at; accepted_or_rejected_by; disposition_at; authority; integrity_ref; result; limitations; side_effects_observed; related_record_ids; state`

States: `captured -> verified -> accepted | rejected | invalid | stale`. Name observer, verifier, and acceptor separately: observation does not imply verification, and verification does not imply disposition. Apply the predeclared independence rule before identities may coincide. An artifact's existence is not verification; acceptance requires the referenced criteria, claim, context, observer, and limitations to match.

## SSoT, manifest, lint, and staleness

- The **SSoT map** assigns each governed fact one current authority, owner, version, and conflict rule. External and repository state remain authoritative for their own facts.
- A **Context Manifest** lists only the versions and evidence needed for the next authorized action: goal, scope, active Decisions, blocking Context Issues, contracts, affected state, authority, and stop conditions.
- **Context Lint** continuously detects missing provenance, conflicting authorities, stale references, orphaned decisions, unauthorized state, incomplete records, and obsolete active context. Lint reports findings; it does not rewrite truth.
- Any cleanup, migration, or refactor is a reviewed Atomic Change Issue with regression evidence. A passing lint result is detection evidence, not customer acceptance.

When a Decision is superseded or evidence invalidates a dependency, traverse `affected_nodes` and dependencies through SSoT entries, manifests, contracts, E2E, tests, changes, evidence, deployed state, and external effects. Mark each dependent `stale` or `blocked`, stop unsafe work, identify the last consistent state, and reopen the earliest affected gate.

## Live work and side effects

Before changing an in-progress, deployed, or externally effective system, inventory the actual state and owner. Do not assume repository, plan, deployed version, and external state agree. If authority, state, or recovery is uncertain, stop cleanly and preserve evidence.

Choose and pre-authorize the recovery action: **stop** before effect; **rollback** a reversible internal change; **compensate** an irreversible external effect with a new traceable action; or **reconcile** divergent authoritative records. Record partial completion and idempotency boundaries. Never label a failed mutation atomic until consistency is restored or the inconsistency is explicitly owned and blocked.

## Control rules

- Fail closed on missing authority, contradictory SSoT, unowned risk, absent evidence, unsafe dependency, or unverifiable side effect; state the exact resumption condition.
- Preserve isolation: one atomic purpose cannot silently alter another unit, and independent reviewers cannot inherit the implementer's conclusion as evidence.
- Preserve durability: approved Decisions, evidence, acceptance, rollback, compensation, and reconciliation remain traceable after active context is cleaned.
- Minimize context, records, dependencies, changes, and gates instantiated for the current outcome. Formal volume, issue counts, test counts, or successful self-review are never value.
