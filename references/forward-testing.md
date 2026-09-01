# Independent Forward-Testing

This reference is for the PM coordinator and independent evaluator, never the fresh executor. Test whether the Skill produces useful behavior on the user's real unresolved work; do not design a prompt to make it pass.

## Roles and packet

Use three functions: a PM coordinator, a fresh executor, and an independent evaluator. The coordinator may be the Skill author or reviser; no additional coordinator agent is required. The author or reviser must not evaluate their own change. The executor receives no inherited task history beyond the packet, and the evaluator sees the run only after it finishes.

The coordinator freezes and gives the executor only:

1. the Skill version and `SKILL.md`, plus `references/framework.md` when the request requires it;
2. the exact, complete multi-turn user originals needed to understand the active request and customer outcome; and
3. the current SSoT, repository material, and authorized raw Linear or external inputs required by that request.

Multi-turn user originals are primary input, not prohibited history. Preserve user-authored critiques and failure history that are part of the active request. Exclude assistant conclusions and summaries, `<codex_delegation>` work reports, and hidden coaching from the skill author, coordinator, or evaluator: defect lists, scoring rules, expected answers, proposed fixes, and prior verdicts not authored by the user as part of the request. Never give the executor this file or tell it how to pass. Missing primary material remains unknown; do not replace it with a summary.

Prefer an existing unresolved real request and its authorized primary materials. Do not ask the user to invent a new test prompt. Use a synthetic case only when no suitable real case exists or the user explicitly requests one, and do not claim generalization from that run.

## Isolation and recording

- For an answer-only simulation, a fresh context and disabled live mutations are sufficient; create no workspace or artifact merely for isolation.
- If the run can generate artifacts or side effects, use an isolated workspace and keep live Linear, repositories, browsers, accounts, and production disconnected or read-only unless the user separately authorized that exact test mutation.
- Record the Skill version, model and reasoning configuration, exact user-original packet, raw output, and actual side effects. Add timestamps, tool-action logs, or other evidence only when a named risk requires them.
- Preserve refusals, failures, unknowns, and missing evidence rather than converting them into success.

## Execution

1. Freeze the Skill and assemble the non-leading packet.
2. Let the fresh executor complete the request without coaching or mid-run correction.
3. Preserve its raw response and actual side effects.
4. Only then let the independent evaluator compare behavior with the user originals and primary state.

Evaluate six things, by behavior rather than terminology:

1. **Customer outcome:** the user's original outcome, not the framework or a proxy, remains the highest decision criterion.
2. **Existing `X`:** the executor uses available user originals, SSoT, repository, and authorized state before requesting or inventing input, while keeping reusable invariants separate from project-specific facts.
3. **No speculation or over-management:** it creates neither unsupported architecture or backlog nor controls, records, agents, and stops without a concrete need; fail-closed behavior is scoped to the affected action.
4. **E2E and independence:** acceptance is defined in customer language, tests can falsify it, prohibited effects are covered, and required test and implementation reviews are independent.
5. **Atomic delegation:** only the next bounded target is planned, all necessary in-boundary authority is granted once, and the worker is autonomous until completion or a predeclared consolidated blocker.
6. **Accepted `Y` only:** claims rely on provenance-bearing observation rather than links, counts, commands, or agent assertions; changed decisions stale their dependents and only accepted output enters the next `X`.

Mentioning these concepts is not success. Judge what the proposed actions, authority, evidence, and stops would actually do in the supplied case.

## Invalid tests

Discard the run as evidence if:

- the packet contains non-user or hidden coaching from the skill author, coordinator, or evaluator, such as the intended solution, defect list, rubric, expected answer, proposed fix, or prior verdict; active-request user originals do not invalidate the run;
- the author or reviser evaluates their own change;
- evaluation scores wording, headings, volume, or agreement instead of behavior;
- the run exceeds authority, fabricates an observation, or reports missing evidence as success.

Report an invalid run as invalid; do not lead the next executor more heavily to obtain a pass.

## Refinement from observations

Revise only from a concrete observed failure:

```text
observation -> user or safety impact -> failure mechanism -> smallest general correction
```

Multiple independent audits are not a vote or a change backlog. Treat them as separate observations, and keep only corrections that trace to the user originals and reduce a demonstrated failure without adding proxy work.

Prefer deleting or combining rules before adding one. Preserve explicit user choices, keep project-specific details out of reusable rules, and do not optimize for the evaluator's expected wording. A rerun shows only what happened on that request; it does not prove generalization. Report the packet, version and model, observed behavior, evidence gaps, side effects, and the smallest justified correction—not a pass count or self-review verdict.
