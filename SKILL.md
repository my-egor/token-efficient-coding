---
name: token-efficient-coding
description: Use when the user explicitly invokes $token-efficient-coding or says "включи режим экономии" for a software-engineering task; routes work with minimal context and evidence-based escalation.
---

# Token-efficient coding

Optimize the current software-engineering task for low context usage and the least expensive sufficient model without weakening correctness or authorization boundaries.

## Activation boundary

Activate only when the user explicitly invokes `$token-efficient-coding` or gives the instruction `включи режим экономии`. The mode applies to the current task only.

Discussion about tokens, model prices, orchestration, or economy without one of those instructions does not activate the workflow.

At activation, give one short notice after inspecting enough context to classify the task:

`Режим экономии включён: <SMALL|MEDIUM|HIGH>, <маршрут>.`

## Route by evidence

| Lane | Observable conditions | Route |
| --- | --- | --- |
| SMALL | Local, low-risk, easily verified change; usually one or two related files | Complete in the coordinator. Do not spawn a subagent. |
| MEDIUM | Bounded feature, ordinary debugging, or several related files without high-risk impact | Use at most one isolated Luna or Terra implementer when delegation is genuinely cheaper than coordinator execution. |
| HIGH | Architecture, authentication, security, destructive migration, broad cross-cutting change, or substantial unresolved uncertainty | Use one isolated Sol implementer. Use Astra only for a concrete highest-capability need or after a lower lane demonstrably fails. |

Use risk and uncertainty, not prompt length, to classify. A clear local test failure remains in its current lane.

Before selecting a subagent, inspect the current `spawn_agent` allowlist. Set both `model` and `reasoning_effort` explicitly. Never invent or reuse a stale model name. If the preferred model is unavailable, select the least expensive suitable available model.

## Delegation contract

Delegate only when it reduces expected total work. Default to one implementer and no separate reviewer. Parallel agents are appropriate only for independent workstreams likely to reduce total work, not merely elapsed time.

Use `fork_turns: "none"` by default. Use a small positive turn count only when recent user text is essential and cheaper than restating the bounded brief. Never copy the full transcript merely for convenience.

Send a compact brief containing only:

```text
Outcome: <observable requested result>
Scope: <project path and relevant files or search boundary>
Constraints: <authorization, compatibility, and do-not-change boundaries>
Done when: <observable acceptance criteria>
Verify: <commands to run, or how to discover the project commands>
Return: outcome, changed paths, verification evidence, unresolved issues
```

Do not paste file contents the implementer can read directly. Ask it not to restate the request or narrate routine exploration.

## Execute and verify

1. Inspect the real repository state and the smallest relevant scope.
2. Classify the task and choose the route.
3. Implement with the coordinator or at most one implementer by default.
4. Inspect the actual diff and repository status.
5. Run relevant tests, build, compiler, type checker, linter, or formatter commands.
6. Report unavailable or failing checks honestly.
7. Declare completion only when the requested behavior, scope, and relevant deterministic checks are satisfied.

Use software for facts. Do not spend a model call asking whether a test, compiler, type checker, formatter, or diff probably passes.

## Retry before escalation

When a repair is needed, continue the same implementer with `followup_task` and send only the new failure evidence and the bounded correction request. Do not spawn a replacement merely to obtain a fresh attempt.

Escalate only after an observable trigger:

- repeated attempts fail;
- the cause remains unclear after bounded investigation;
- architectural or security impact is newly discovered;
- the change grows materially beyond the original scope;
- the current model identifies a concrete unresolved uncertainty.

A failing check whose cause is clear and locally repairable is a retry, not an automatic escalation.

## Common mistakes

- Spawning for a SMALL task adds context and coordination cost.
- Copying the entire conversation defeats context isolation.
- Adding a reviewer to every task spends tokens without proportional value.
- Replacing an implementer discards useful context; resume it instead.
- Using model judgment for deterministic facts adds cost without evidence.
- Claiming token savings without measured usage is not verification.
