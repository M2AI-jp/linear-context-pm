# Linear Context PM Framework v0.5.4

Read this reference when designing, simulating, onboarding, or auditing a Linear-centered context system. It defines the reusable kernel; it does not prescribe a product's technology or architecture.

## 1. Intended outcome

The top-level outcome is to keep project-specific `X` clean enough for the next Codex session to act from current truth. `X` has two layers: durable project memory in Linear/SSoT, and the active execution context injected into the current worker/session. Linear externalizes the procedures and state transitions that protect `X`; it must preserve the planning horizon without forcing all of that scope into the active execution context. SSoT, E2E, Issue decomposition, Git-state linkage, independent review, QA, stale cleanup, and worker authority are mechanisms under that purpose, not parallel goals.

The framework must preserve this invariant:

```text
Y may enter project memory or active execution context only when its claim, evidence, and approval have passed
the gate declared before Y was produced.
```

Store enough raw evidence to reconstruct events, but inject only current, authoritative, task-relevant context into an agent session. More retained data must not imply more injected context. Minimize active execution context, code, files, dependencies, cost, and simultaneous execution. Do not minimize away Linear state records, review work, or decomposition that protects `X` by isolating real responsibilities, failure ranges, dependencies, consumers, acceptance paths, or external side effects.

Every work object must make these fields explicit:

- actor or owner;
- input and its authority;
- process or decision rule;
- output and status;
- consumer or downstream object that will use the output;
- intended and observed side effects;
- dependencies;
- required permission and approver;
- evidence and counterevidence;
- acceptance path into project memory or active execution context;
- stop condition and recovery path.

## 2. Common Kernel and Project Profile

### Common Kernel

The Common Kernel defines only reusable governance semantics:

- context declarations and authorization boundaries;
- gates and state transitions;
- Context Issues, Decisions, SSoT, Context Manifests, and Atomic Change Issues;
- evidence envelopes and acceptance;
- stale propagation, rollback, compensation, and reconciliation;
- Context Lint and context refactoring;
- E2E-before-implementation and independent review;
- minimum-scope, fail-closed, and anti-proxy rules.

Do not place product providers, model names, frameworks, folder names, data schemas, or UX assumptions in the Common Kernel.

### Project Profile

A Project Profile instantiates the kernel for one target. Derive it from evidence rather than analogy. It may define:

- customer outcome, actors, boundaries, and non-goals;
- source repositories and non-repository systems;
- technology stack and exact versions;
- SSoT locations and precedence;
- external services, environments, identities, permissions, and secrets boundaries;
- data, interaction, interface, and failure contracts;
- risk-specific E2E and human acceptance;
- module boundaries, dependency directions, and repository layout;
- the mapping from Atomic Change Issue to a concrete change unit;
- lint, test, evidence, release, rollback, retention, and privacy policy.

Project-specific facts remain unknown until a user or authoritative source confirms them. A simulation must show where they would be learned; it must not invent them.

## 3. Linear object model

Read the objects below as a dependency chain, not a menu: the Goal defines the customer outcome; Gates control lifecycle state; Context Issues and Decisions remove uncertainty; SSoT and Context Manifest define current truth and active execution context; Atomic Change Issues and checkpoints bound execution; Evidence decides whether an output may enter the next `X`.

Use Linear's native structures first: Issues for individual work, Projects for customer outcomes, Milestones for meaningful stages or checkpoints, team workflow statuses for state, and configured Git integrations for PR or commit links. Rely on automation only after the current workspace shows it is configured. "Smallest" means the least custom machinery, not fewer useful Issues. If Linear planning is authorized for a known scope, preserve or create the Issues needed to represent that scope while keeping non-current checkpoints inactive.

Before any Linear planning mutation, declare both horizons:

- **Planning horizon:** the customer outcome, product slice, or project scope that Linear must represent.
- **Execution horizon:** the single checkpoint or work boundary currently authorized to run.

A request to create an implementation plan, project, or backlog for a named outcome sets the planning horizon to that outcome unless the user explicitly narrows it. A phrase such as "proceed until SSoT" or "current checkpoint only" limits the execution horizon, not the planning horizon.

Then create a coverage ledger for the planning horizon. Each row records the scope item, classification (`current execution`, `inactive planned`, `unknown`, or `excluded`), representing Issue, consumer or acceptance path, and omitted reason. Do not mutate Linear if an in-scope item is only named in a Project, Milestone, Document, coverage row, or checkpoint title, postponed because execution is not yet authorized, or omitted without evidence that it is duplicate, invalid, stale, or out of scope. Unknown or unaccepted scope that matters to the planning horizon still needs a Context Issue or contract/E2E Issue; it is not a reason to create no Issue.

If an existing or archived plan exists, inventory its decomposition before replacing it: responsibilities, failure ranges, dependencies, consumers, acceptance paths, and issue count only as a degradation signal. Do not compress real coverage into broader units unless the user explicitly chooses reduced scope or the old unit is proven duplicate, invalid, or stale. A bad old plan may be abandoned, but useful coverage must be preserved or deliberately superseded by finer, cleaner decomposition.

### Goal or Project

Represents one independently acceptable customer outcome. Infrastructure without independent customer value belongs inside the outcome's gates or module checkpoints unless the Project Profile establishes a real separate consumer.

### Gate

Controls transition between lifecycle stages. Every Gate records:

- required inputs;
- required outputs;
- named owner;
- named approver who did not produce the accepted output when independence matters;
- observable exit criteria;
- failure and stop conditions;
- downstream objects invalidated by later change.

### Context Issue

Resolves one blocking unknown or one decision. It does not exist merely to make discovery look complete. Required fields:

- one question or decision;
- why it blocks a named Gate;
- allowed sources and read/write authority;
- investigation owner;
- required primary evidence;
- output Decision or confirmed fact;
- affected SSoT;
- exit and stop conditions.

### Decision

Records a selected option, not a discussion transcript. Required fields:

- decision statement and status;
- author and approver;
- effective time and scope;
- inputs and evidence;
- rejected alternatives only when they explain the choice;
- affected objects;
- predecessor Decision, when superseding;
- rollback or migration consequences.

Never edit history to make an old Decision appear current. Create a successor with `supersedes`, mark the predecessor `Superseded`, and trigger impact analysis.

### SSoT

An SSoT is the authoritative current definition for one information class. Define an authority map that states which system owns goals, product behavior, code, tests, runtime state, and external state. Avoid copying the same current rule into several authoritative locations.

### Context Manifest

A Context Manifest is the minimal, reproducible input set for one task or session. Record:

- task and Gate;
- included sources with revisions;
- reason each source is included;
- explicit exclusions;
- unresolved unknowns;
- permissions and prohibited effects;
- expected output and acceptance route;
- expiry or invalidation conditions.

### Atomic Change Issue

Represents one responsibility and one independently reviewable change target.

- **Code Profile:** one Atomic Change Issue equals one file. Create separate issues for production code, tests, SSoT, or configuration files. Bundle the justified set into one module PR checkpoint.
- **Browser or SaaS Profile:** one issue equals one operation purpose or one configuration object, with before/after evidence and idempotency or compensation.
- **Document Profile:** one issue equals one document or one bounded content responsibility.
- **Other Profiles:** choose one bounded unit with one change reason, explicit side effects, and a recoverable boundary.

Do not force a non-code action into a file-shaped issue. Do not decide filenames or create Atomic Change Issues before contracts and module responsibilities are accepted. After the relevant scope, contracts, and acceptance are accepted, create every justified atomic Issue for the known decomposition, including production files, test files, SSoT or configuration files, independent test-review work, implementation QA work, non-code operations, and Git-state transitions when each has its own failure range. A checkpoint or title never substitutes for its required atomic Issues.

### Module or PR checkpoint

For a code profile, a checkpoint is one loosely coupled module and contains the required one-file Issues plus required Git-state Issues. Its acceptance bundle includes:

- applicable linter results;
- tests defined before implementation;
- independent qualitative review of those tests;
- implementation changes;
- independent implementation QA;
- regression and integration evidence proportionate to risk;
- branch, PR, review handoff, merge, main promotion, rollback, or reconciliation state when applicable;
- rollback point and unverified scope.

A green PR, commit SHA, or number of checks is metadata, not acceptance by itself.

### Evidence envelope

An evidence reference must state what it proves. Record:

```yaml
claim: "The exact proposition being evaluated"
source_id: "Stable primary-source identifier"
observed_at: "Timestamp with timezone"
subject_revision: "Commit, configuration revision, model/prompt version, or object version"
environment: "Where the observation occurred"
run_or_correlation_id: "Traceable execution or operation identifier"
observer: "Actor that captured the evidence"
adjudicator: "Independent role that accepted or rejected the claim"
result: "pass | fail | unknown | conflicting"
counterevidence: "Observation that would falsify, or did falsify, the claim"
side_effects: "Observed external changes"
pii_and_retention: "Sensitivity, redaction, access, and retention policy"
location: "Link to retained primary evidence"
```

The ID, link, screenshot, status badge, or generated summary alone is insufficient. Missing observation, mismatched revision, inaccessible source, or conflicting evidence results in `unknown` or `blocked`, never inferred success.

## 4. Lifecycle and gates

The Gate sequence is a dependency order, not a mandate to create every possible artifact. Skip a Gate only when the Project Profile records why its risks do not apply.

### G0A — Provisional charter

- **Input:** user's current request and explicit constraints.
- **Process:** distinguish confirmed facts, proposals, unknowns, authority, and prohibited effects.
- **Output:** provisional purpose, investigation scope, read authority, prohibited operations, owner, and provisional stop conditions.
- **Owner:** PM.
- **Approver:** user or named sponsor for scope and authority.
- **Exit:** read-only inventory can proceed without inventing final scope or causing external effects.
- **Stop:** even read access is unauthorized, scope cannot be bounded, or instructions conflict materially.

### G1 — Read-only Context Inventory

- **Input:** accepted G0A.
- **Process:** inspect only authorized primary sources, repositories, runtime descriptions, external-system metadata, prior Decisions, and known evidence.
- **Output:** source inventory, authority map draft, contradictions, stale candidates, missing access, and only the unknowns that block G0B or the next Gate.
- **Owner:** investigator.
- **Approver:** PM; a domain owner confirms disputed facts.
- **Exit:** current evidence and uncertainty are traceable; no mutation occurred.
- **Stop:** a required source is unavailable, an external read needs new authority, or sources conflict without a named resolver.

### G0B — Final outcome, scope, and authority

- **Input:** G0A and G1 inventory.
- **Process:** establish the customer outcome, acceptance owner, project boundary, non-goals, permissions, budget, risk, and termination conditions.
- **Output:** accepted charter, planning horizon, execution horizon, and prioritized blockers.
- **Owner:** PM.
- **Approver:** user or sponsor.
- **Exit:** one observable outcome and its non-goals are accepted; responsibility and authority are explicit.
- **Stop:** the outcome is not observable, the approver is absent, or mutually incompatible goals remain.

### G2 — Project contracts and Decisions

- **Input:** accepted G0B and blocking Context Issues.
- **Process:** resolve only the technical, data, interface, environment, permission, evidence, privacy, and recovery decisions required for the current outcome.
- **Output:** accepted Decisions and Project Profile contracts, including exact stack only where now justified.
- **Owner:** relevant domain owner coordinated by PM.
- **Approver:** named accountable owner; security or product approver where applicable.
- **Exit:** the next stage does not need to invent a material contract.
- **Stop:** a blocking unknown lacks evidence or approval.

### G3 — SSoT, Context Manifest, and Context Lint

- **Input:** accepted contracts and source inventory.
- **Process:** establish the authority map, minimal SSoTs, repository instructions where applicable, task manifest, and lint rules; detect contradictions and stale active execution context.
- **Output:** validated project memory, active execution context, lint findings, and atomic cleanup candidates.
- **Owner:** context steward.
- **Approver:** PM plus relevant SSoT owner.
- **Exit:** required sources are current, non-duplicative, reachable, and sufficient for E2E definition.
- **Stop:** conflicting authorities, unresolved stale rules, missing required sources, or an unsafe cleanup proposal.

### G4 — E2E and qualitative test review

- **Input:** accepted customer outcome, contracts, SSoT, and manifest.
- **Process:** define E2E in customer language before implementation; define tests and have an independent reviewer assess whether the tests actually prove the outcome and reject forbidden effects.
- **Output:** accepted E2E, test artifacts or test plan, evidence requirements, counterevidence, and qualitative review.
- **Owner:** test author who is not the implementation owner when feasible.
- **Approver:** independent test reviewer and product acceptance owner.
- **Exit:** tests cover observable success, failure, forbidden outcomes, side effects, and risk-relevant regression without encoding the proposed implementation as the answer.
- **Stop:** test success can be achieved without customer success, test evidence is unverifiable, or independence is compromised.

### G5 — Atomic plan and module checkpoints

- **Input:** accepted G4 and module contracts derived from current requirements.
- **Process:** derive issues from accepted E2E, contracts, module boundaries, artifact roles, and state transitions. First make the coverage ledger; then split the work whenever owner, target, input authority, consumer, permission, evidence, side effect, failure mode, rollback path, or review role differs. Then identify dependency direction, module checkpoints, rollback, and permitted parallelism.
- **Output:** planning horizon, execution horizon, coverage ledger, and fine-grained decomposition for the planning horizon at its current maturity, with only the current checkpoint execution-authorized. Non-current checkpoint Issues remain in Linear as inactive planning records; they are excluded from active execution context and execution prompts until their checkpoint is opened.
- **Owner:** PM or architect acting within accepted contracts.
- **Approver:** PM and module owner.
- **Exit:** every change maps to an accepted test or necessary enabling contract, has one responsibility, and has no hidden cross-module effect.
- **Stop:** a change crosses responsibility boundaries, modifies a protected path without regression evidence, or exists only for hypothetical reuse.

### G6 — Execute and independently verify

- **Input:** a Ready Atomic Change Issue, accepted manifest, pre-reviewed test, and permissions.
- **Process:** PM gives the worker the complete boundary and required authority for that boundary. The worker changes only its owned target and proceeds without stepwise approval unless a stop condition is reached. Independent QA assesses implementation, lint, tests, dependency boundaries, and regression evidence.
- **Output:** verified or rejected change bundle with evidence envelope and unverified scope.
- **Owner:** worker for the change; QA for verification.
- **Approver:** PM or module approver who did not self-certify the implementation.
- **Exit:** the checkpoint's predeclared criteria pass against the exact revision and environment.
- **Stop:** scope expands, context changes, evidence is missing, worker and reviewer independence collapses, or external state diverges.

### G7 — Real-environment acceptance

- **Input:** verified module result and accepted evidence plan.
- **Process:** observe the customer outcome and required external side effects in the authorized environment; read back external state when applicable.
- **Output:** accepted, failed, unknown, or conflicting result with primary evidence.
- **Owner:** release or acceptance operator.
- **Approver:** product acceptance owner; human acceptance where the Project Profile requires it.
- **Exit:** the outcome and forbidden outcomes are adjudicated for the exact released state.
- **Stop:** only synthetic/proxy evidence exists, observation is incomplete, correlation is lost, or production authority is absent.

### G8 — Close and produce next X

- **Input:** G7 result, all Decisions, changes, evidence, and observed side effects.
- **Process:** reconcile Linear, Git/CI, deployed state, and external state; supersede obsolete Decisions; remove stale material from active context; archive necessary history; create the next minimal manifest.
- **Output:** consistent accepted state, open failures or compensations, and clean next `X`.
- **Owner:** PM and context steward.
- **Approver:** acceptance owner plus affected external-state owner.
- **Exit:** no partial success is hidden, active SSoT matches accepted reality, and remaining work is explicit.
- **Stop:** an external side effect cannot be reconciled, rollback or compensation is incomplete, or accepted state conflicts with primary evidence.

## 5. State models

Use semantic states even when Linear must represent them with its native workflow and labels.

### Gate

```text
Draft -> Ready -> In Progress -> Review -> Accepted
                    |             |
                    +-> Blocked <-+
Accepted -> Superseded
```

Only required input permits `Ready`; only exit evidence permits `Accepted`.

### Context Issue

```text
Proposed -> Ready -> Investigating -> Evidence Review -> Resolved
              |            |                |
              +----------> Blocked <--------+
Resolved -> Stale | Superseded
```

`Resolved` means the question has an accepted answer or explicit `unknown`; it does not mean the desired answer was found.

### Decision

```text
Draft -> Proposed -> Accepted -> Superseded
                   -> Rejected
Accepted -> Disputed -> Accepted | Superseded
```

Never mutate the meaning or evidence of an accepted Decision in place.

### Atomic Change Issue

```text
Planned -> Ready -> In Progress -> Independent Review -> Accepted -> Applied -> Closed
             |             |              |               |
             +----------> Blocked <-------+-------------> Reverted
Accepted | Applied | Closed -> Stale
```

`Applied` means the intended target changed. `Closed` additionally requires checkpoint reconciliation; neither implies customer acceptance unless G7 passed.

### Linear workflow mapped to Git

For repository work, define a Project Profile mapping from Linear workflow states to Git and review state before execution:

- `Todo`: the Issue contract is valid and no worker has begun the target.
- `In Progress`: the assigned worker is changing the one file or one non-code target.
- `In Review`: the PR is open or the independent test review / implementation QA is pending.
- `Blocked`: SSoT, acceptance, Git state, issue boundary, authority, or evidence contradicts the planned transition.
- `Done`: the relevant PR has been merged to main or the external change has been reconciled, independent review evidence is referenced, and the PM/acceptor has accepted the exact claim.

Only the authorized mover defined in the Project Profile may change each state. An open PR, passing command, clean merge state, or unconfigured check is not enough for `Done`. A Project is not Completed until the declared customer/user outcome is accepted, not merely because setup or an entry checkpoint passed.

## 6. Supersession, stale propagation, and external state

Maintain an impact graph between Decisions, SSoTs, manifests, E2E, tests, Atomic Changes, module checkpoints, evidence, deployed revisions, and external objects.

When an accepted Decision changes:

1. create and approve the successor Decision;
2. mark the predecessor `Superseded`, without rewriting it;
3. mark dependent active objects `Stale` until revalidated;
4. freeze affected Ready and In Progress work;
5. determine whether merged code or deployed state must be rolled back, migrated, or retained temporarily under an explicit exception;
6. identify external side effects that require compensation, idempotent retry, or readback reconciliation;
7. invalidate evidence whose revision, environment, or assumption no longer matches;
8. update active SSoT only through an authorized atomic change;
9. regenerate the affected Context Manifest after consistency is restored.

Never delete evidence needed to explain or repair an external side effect. Remove obsolete material from current SSoT/Manifest and active execution context; retain only the necessary history in a clearly non-authoritative archive.

## 7. Context Lint and refactoring

Context Lint detects; it does not silently rewrite. Project Profiles enable only rules with current value. Candidate checks include:

- conflicting or duplicated active authorities;
- stale references after Decision supersession;
- active instructions pointing to archived code, tests, or plans;
- broken evidence links or evidence/revision mismatch;
- completed claims without an evidence envelope;
- unexecuted, flaky, synthetic, or unknown results represented as pass;
- Linear status inconsistent with Git/CI, deployed state, or external readback;
- Context Manifest sources that are irrelevant, expired, unauthorized, or missing;
- secrets, PII, or untrusted external instructions entering agent context;
- cross-module dependencies, shared mutable state, or responsibility dumping;
- tests that encode stale behavior or can pass without the customer outcome.

Treat a cleanup rewrite as an Atomic Change Issue. It requires:

- the detected defect and affected authority;
- a bounded target;
- preservation or migration rule;
- regression evidence;
- independent review;
- rollback or recovery.

Do not call file-count, line-count, issue-count, test-count, coverage, or lint-count reduction a successful refactor without evidence that the active context became more correct and the accepted behavior remained intact.

## 8. E2E, tests, and independent review

Define E2E before implementation in the language of the external actor. Each scenario identifies:

- actor and precondition;
- input or action;
- observable journey;
- observable result;
- permitted and forbidden side effects;
- interruption, failure, and recovery behavior;
- environment and evidence source;
- falsification condition;
- acceptance owner.

Test artifacts precede implementation artifacts. In a code profile, each test file is its own File Issue. The qualitative test reviewer receives the goal, accepted contracts, SSoT, and tests, but not a proposed implementation as an authoritative answer. The reviewer checks whether:

- the test can pass while the customer outcome fails;
- mocks, fixtures, injected state, or assertions bypass the real path;
- only favorable cases are measured;
- forbidden side effects and regressions remain observable;
- the claimed environment and evidence are genuine;
- acceptance criteria were weakened after seeing results.

Implementation workers do not self-QA. Independent QA reviews the exact change and exact tests after implementation. The PM adjudicates scope and evidence but does not turn its own plan into proof.

Synthetic, replay, mock, static, staging, production, and human evidence are distinct. One may replace another only when the accepted Project Profile explicitly establishes equivalence.

## 9. Logging and evidence boundaries

- Git and CI own source changes, diffs, commits, test output, lint output, and raw development execution logs.
- Linear owns PM state, decisions, approval, blockers, evidence envelopes, and links to primary records.
- External systems own their actual runtime or configuration state; Git intention is not external fact.
- Browser, SaaS, human, agent, and production operations outside Git receive primary evidence with actor, before/after state, correlation, side effect, and authority.
- Summaries remain secondary. Preserve a route to the primary evidence.
- Do not paste every raw log into Linear or inject it into every session.

## 10. Minimum-scope and anti-reward-hacking rules

- Create only Context Issues that block the current Gate or the authorized decomposition of the planning horizon.
- Do not create implementation Issues from unknown scope, unaccepted contracts, speculative integrations, placeholder providers, abstractions, or recovery machinery. Unknown or unaccepted scope inside the planning horizon receives Context Issues or contract/E2E Issues until it matures. Once scope, contracts, and acceptance are accepted, create the non-current checkpoint Issues as inactive planning records; future execution being unauthorized must not mean future decomposition is omitted.
- When scope, contracts, and acceptance are known and Linear planning is authorized, decompose the known scope into inactive atomic Issues before execution; do not collapse them into checkpoint titles.
- Derive module and file issues only after the relevant contract and test are accepted, then derive all required Issues for the authorized known decomposition, not just the next file that happens to be executed.
- Automate a lint or workflow only when the rule is deterministic enough and repetition justifies its cost.
- Add a review, check, artifact, or safety gate only when it names the risk it controls and the result can change a Linear state, authority boundary, active execution context, or release decision.
- Use manual review for novel qualitative judgment; do not fabricate a score to make it automatable.
- Issue count, story points, completed gates, files, agents, tests, coverage, commits, checks, dashboards, and evidence links are not customer value. Issue-count reduction is also not customer value. More Issues are correct when each one isolates a real responsibility, failure range, dependency or consumer, and acceptance path.
- Never alter evaluation prompts, criteria, tests, or evidence after seeing output merely to obtain a pass.
- Never let the same output authorize itself, test itself, and approve itself.
- Prefer a clean stop and an explicit unknown over an invented assumption or ceremonial completion.

## 11. Designing or simulating a project

When asked how Linear would be structured for a project from zero:

1. declare current confirmed context, proposals, unknowns, authority, and stop conditions;
2. show the Common Kernel separately from the Project Profile;
3. if scope is still unknown or unauthorized, create only the provisional Goal/Project and G0A/G1/G0B blockers justified now;
4. declare the planning horizon and execution horizon; if the request asks for a project or implementation plan, do not let a "work until SSoT/current checkpoint" phrase shrink the planning horizon unless the user explicitly says not to create later-scope Issues;
5. if the planning horizon is authorized, produce the coverage ledger, checkpoint map, and appropriate Issues for that horizon before execution begins or Linear is mutated; use Context or contract/E2E Issues for unknown/unaccepted parts, and Atomic Change Issues for accepted parts;
6. mark exactly one checkpoint as execution-current and leave later Issues inactive until their checkpoint is opened;
7. show evidence envelopes, stale propagation, fail-closed behavior, Git/Linear state transitions, and cleanup into the next `X`;
8. state explicitly which technologies, files, external mutations, and execution authorities are still not created or not authorized.

A useful simulation demonstrates how the framework discovers project-specific facts. It does not masquerade invented project detail as a complete implementation plan.
