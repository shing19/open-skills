# Task contract

Give each subagent a self-contained, bounded packet:

```text
Task ID:
Objective:
Why this task exists:

Allowed inputs and evidence paths:
Owned files and non-file resources:
Expected output or return schema:
Dependencies:

Assigned model tier and reasoning effort:
Timeout or check-in condition:

Constraints and forbidden actions:
Acceptance checks:

Required return:
- concise result
- changed artifacts
- commands/checks with exit status
- evidence pointers
- unknowns and residual risks

Escalate when:
```

Do not include the full parent conversation. Include the execution-document path for orientation, but do not authorize the subagent to edit it.

## Sizing

A task is ready when one Agent can complete it in one bounded run and the main Agent can accept it without reconstructing another project.

Split when it has multiple independent results, unrelated resources, incompatible evidence types, safe parallel dependencies, or partial failure would be hard to reconcile.

Do not split when the pieces would repeatedly read the same evidence, edit the same resource, or require the main Agent to reassemble trivial fragments.

If the assigned task is too large, return:

```text
status: replan_requested
reason:
proposed_subtasks:
partial_state_or_side_effects:
resources_still_owned:
```

Do not recursively spawn subagents unless the task packet explicitly authorizes nested orchestration.

## Resource ownership

Assign one writer for every mutable file, directory, Git branch, database, queue, API object, cloud service, deployment slot, shared document, issue, pull request, release, or remote configuration.

Read-only access may overlap. Mutation may overlap only when the system has an explicit reconciliation or transactional mechanism.

## Model tiers

### Low tier

Use the configured low tier for inventory, retrieval, classification, mechanical transforms, schema checks, and other work with an explicit answer surface.

### Medium tier

Use the configured medium tier for bounded implementation, focused debugging, test writing, and local analysis with clear constraints.

### Strong tier or main Agent

Use for architecture, security, finance, permissions, irreversible external state, ambiguous synthesis, and work whose errors are hard to detect.

Model choice is a dispatch parameter, not an `agents/openai.yaml` setting. Inspect the current host schema and follow the configured fallback when an override is unavailable.

## Concurrency and review budget

Dispatch only ready tasks with disjoint mutable resources. Stop new dispatch at the configured returned-but-unaccepted limit, reduce the limit for high-risk outputs, and never reassign a stale task's resources until actual state is reconciled.

## Return packet

Prefer:

```text
status: completed | blocked | replan_requested
result:
artifacts:
checks:
  - command_or_check:
    exit_status:
    key_result:
evidence:
unknowns:
risks:
recommended_next_action:
```

Keep full logs and large diffs in files or tool state. Provide stable paths and the smallest key excerpt needed to interpret them.
