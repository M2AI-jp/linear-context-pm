# Independent Forward-Testing — Coordinator/Evaluator Only

This reference is only for the test coordinator and post-run evaluator. Never give it to the fresh executor. Use forward-testing to observe whether this skill changes an independent agent's decisions safely. It is not a wording test and must not be shaped to certify a desired result.

## Independence boundary

Keep Skill author/reviser, coordinator, fresh executor, and post-run evaluator as separate roles. The author is neither executor nor evaluator. The coordinator freezes the Skill version and input packet before execution and does not coach, correct, or supply intermediate hints. The evaluator reviews only the completed run and preserved primary artifacts; it does not alter the executor's task.

Give the fresh executor only:

1. the frozen `SKILL.md`;
2. the user's unmodified realistic request;
3. `references/framework.md` only when the task itself requires it; and
4. the minimum raw primary artifacts genuinely needed by that request.

Do **not** give the executor this `forward-testing.md`, conversation history, an expected answer, scoring criteria, known defects, proposed corrections, earlier outputs, past conclusions, or a description of how to pass. Do not tell the executor that the Skill is being tested. Do not paraphrase the user request to insert desired behavior. Enforce isolation and permissions through the test environment rather than a coaching brief. If primary material is absent, absence must remain an observable unknown rather than being filled with a summary.

## Isolation and recording

- Use an isolated temporary workspace for generated artifacts.
- Keep live Linear, repositories, browsers, accounts, production, and external data read-only or disconnected unless the user separately authorizes a specific test mutation.
- Use mocks only to contain side effects, never to claim a real outcome.
- Record the exact input packet, Skill version and integrity identifier, model and reasoning configuration, tool/permission boundary, start/end time, raw output, generated artifacts, tool actions, and observed side effects.
- Preserve failures, refusals, unknowns, and missing evidence with the same fidelity as apparent successes.

If isolation or faithful recording cannot be established, do not run the test.

## Execution

1. Freeze and identify the Skill version.
2. Assemble the non-leading packet above without expected results or prior analysis.
3. Start a fresh executor with no inherited task history and no notice that it is participating in a Skill test.
4. Let it complete the realistic request without author intervention.
5. Preserve the actual response, artifacts, actions, stops, and side effects.
6. Only after completion, evaluate observed decisions against the user's request and primary evidence.

The evaluator looks for behavior, not particular headings, words, issue counts, or plan length:

- it separates Common Kernel rules from target-specific Project Profile facts;
- it discovers material unknowns and uses read-only inventory before finalizing scope;
- it stops before unauthorized or under-specified implementation and states a precise resumption condition;
- it creates only next-gate blockers instead of a speculative full backlog;
- it preserves user originals, authority, provenance, and the distinction between confirmed, proposed, unknown, and stale;
- it demands evidence capable of proving or falsifying the customer outcome and rejects links, counts, commands, and agent claims as standalone proof;
- it treats tests as context requiring independent qualitative review and detects bypasses or proxy success;
- it propagates changed Decisions to active work, deployed state, and external effects with stop, rollback, compensation, or reconciliation as appropriate;
- it maps atomic work without assuming code or a particular service, and generalizes safely to non-code systems;
- it keeps the Context Manifest minimal and removes obsolete material from active `X` without erasing necessary history.

A run is not successful merely because it mentions these concepts. Judge whether its proposed sequence, state transitions, evidence, and stops would actually prevent unsupported work and whether it remains minimal for the supplied case.

## Invalid tests

Discard the run as evidence if:

- the executor received the intended solution, defect list, patch plan, earlier verdict, or hidden coaching;
- the Skill author acted as the independent executor or changed the Skill during the run;
- the prompt was rewritten to elicit Skill terminology or match a rubric;
- evaluation scores formatting, keywords, volume, or agreement instead of behavior and artifacts;
- the run touched live state outside explicit authority;
- missing logs, side effects, or evidence were reported as success;
- a claimed observation was fabricated or inferred from an artifact's mere existence.

Report an invalid test as invalid; do not repeat it with a more leading prompt to obtain a pass.

## Version updates from observations

Revise the Skill only from a concrete observed failure. Record:

```text
observation -> user or safety impact -> failure mechanism -> smallest general correction
```

Keep the correction narrow, preserve explicit user choices, and avoid turning one Project Profile's detail into a universal rule. Do not add rules solely to make the tested answer resemble an expected answer. Identify the revised version, then use a fresh independent executor to check the changed behavior under the same unmodified request; use an unseen realistic request as well before claiming broad generalization when that claim matters.

The report must identify the input packet, frozen version, executor configuration, observed output/actions, evidence and gaps, behavioral findings, side effects, and any narrowly justified update. A pass count or self-review is never the conclusion.
