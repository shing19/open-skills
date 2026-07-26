# Orchestration QA

## Before dispatch

- [ ] The execution brief passes the five-item gate.
- [ ] The task has one observable result and explicit acceptance checks.
- [ ] Inputs and evidence paths are accessible.
- [ ] Files and non-file resources have one writer.
- [ ] Dependencies are satisfied and parallel safety is real.
- [ ] Model tier matches complexity, error cost, and acceptance difficulty.
- [ ] Timeout, forbidden actions, and escalation are explicit.
- [ ] The review backlog is below `review_budget`.

## Acceptance evidence

- Retrieval: sources, coverage, counts, unknowns, and traceable conclusions.
- Analysis: inputs, assumptions, criteria, tradeoffs, evidence, and confidence.
- Code: narrow diff, parse/lint/build/test status, inspected behavior, and unrelated state excluded.
- Data: schemas, counts, invariants, samples, rejected data, and reproducible commands.
- External state: exact target, authority, read-after-write proof, user-visible behavior, and rollback.
- Documents: requested structure, audience, resolved references, rendered result when relevant, and facts separated from recommendations.

## Accept and release

- [ ] The main Agent inspected the canonical result, not only the subagent summary.
- [ ] Inspection used the smallest sufficient evidence slice.
- [ ] High-risk or inconsistent evidence received wider inspection.
- [ ] The ledger contains verdict, evidence pointers, residual risk, and rework.
- [ ] Later work uses the checkpoint rather than reloading full logs.

## Recovery and closure

- [ ] Coordinator, task states, running agents, locked resources, Git, and external state agree.
- [ ] Stale resources remain locked until reconciled.
- [ ] Required tasks have accepted or user-approved dispositions.
- [ ] Integrated behavior is accepted as a whole.
- [ ] Canonical owners contain the real outputs.
- [ ] Required commits, pushes, deployments, or external writes are verified.
- [ ] The execution document contains results, residual risks, and rollback.
