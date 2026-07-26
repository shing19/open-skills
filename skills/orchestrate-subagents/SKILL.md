---
name: orchestrate-subagents
description: Orchestrate long-running work through a clean main-agent control plane, a durable execution document, and bounded subagents. Use when the user explicitly asks to organize subagents, delegate execution while the main agent manages and accepts results, split confirmed work across lower-cost workers, or keep the main-agent context clean during a long task. Draft and confirm the execution brief before delegation when scope, authority, deliverables, or acceptance is unclear. Do not trigger for planning-only requests, one atomic task, ordinary parallel tool calls, or merely discussing multi-agent architecture.
---

# Orchestrate Subagents

Run long tasks as a documented control loop. Keep the main Agent focused on the objective, critical path, unresolved decisions, authority, and acceptance. Give execution details to bounded subagents and keep recoverable state in the target workspace.

## Core invariant

The main Agent remains the coordinator and final acceptor. Delegation, an execution document, or a subagent's completion claim is never the requested outcome by itself.

Do not expand user authority through delegation. Keep approvals, scope decisions, high-impact actions, cross-task synthesis, and final acceptance with the main Agent.

## 1. Activate the mode

Trigger on an explicit delegation instruction or a direct continuation of an active execution document. Once activated for a task, keep the mode active until the task finishes or the user asks to stop, take over, or hand it off.

Do not force multi-Agent execution when the work is atomic, cannot be safely partitioned, or would create more review overhead than execution value.

## 2. Initialize execution preferences

Before the first dispatch, read [references/setup.md](references/setup.md). Reuse an existing project or user configuration when present.

If no configuration exists, inspect the host's actual subagent and model-selection capabilities, then ask only for settings that materially affect quality, cost, or safety:

- low-complexity worker model and reasoning effort;
- medium-complexity worker model and reasoning effort;
- high-risk behavior: keep with the main Agent, use a named strong tier, or ask each time;
- maximum worker concurrency and `review_budget`.

Never assume that a public example is the user's preferred model. Never silently substitute a model when the change materially affects cost or quality. If persistent configuration is unavailable, record task-local choices in the execution document.

## 3. Pass the brief gate

Before spawning a subagent, identify one canonical execution document and confirm:

1. the objective has one reasonable interpretation;
2. scope and non-goals prevent obvious drift;
3. deliverables and their canonical owner are explicit;
4. permission and high-risk boundaries are explicit;
5. acceptance can be decided from observable evidence.

If an existing confirmed brief satisfies the gate, use it without asking again.

If no brief exists, copy [assets/execution-document-template.md](assets/execution-document-template.md) into the target workspace and fill it from the conversation. Ask only about missing facts that would change scope, authority, deliverables, or acceptance. Do not make the user write the document from scratch. Wait for confirmation before delegation when any gate item remains ambiguous.

Follow the target repository's planning location and rules. Do not store generic execution state inside this Skill. Keep business artifacts with their canonical project or system.

## 4. Establish the control plane

Record:

- one active coordinator and `updated_at`;
- the objective, done definition, rules, and evidence sources;
- the task graph and resource ownership;
- configured `review_budget`;
- current critical path, ready work, blockers, and next dispatch;
- decisions and compact acceptance entries.

The coordinator is the only writer to the execution document. Subagents edit only their owned artifacts or return a structured result.

Treat coordinator ownership as a cooperative lease, not an atomic lock. If ownership conflicts, stop dispatch, inspect the actual workspace and running agents, then reconcile.

## 5. Create bounded tasks

Read [references/task-contract.md](references/task-contract.md) before the first dispatch or when model choice, concurrency, resource ownership, timeout, or replanning is non-trivial.

Every task must have:

- one observable result;
- allowed inputs and evidence paths;
- owned files and non-file resources;
- dependencies and parallel-safety;
- a configured model tier and reasoning effort;
- acceptance checks;
- forbidden actions and escalation conditions;
- a concise evidence-return contract.

Pass only task-local context. Do not copy the full main conversation into a subagent prompt.

Default to no nested delegation. If a task is too large, the subagent returns `replan_requested`; the main Agent updates the graph and dispatches new bounded tasks.

## 6. Choose models and dispatch safely

Choose by task complexity, error cost, and ease of acceptance:

- use the configured low tier for inventory, retrieval, mechanical conversion, and explicit-schema checks;
- use the configured medium tier for bounded implementation, testing, or local analysis;
- retain high-risk work for the main Agent or the configured strong tier.

High-risk work includes architecture, security, finance, permissions, irreversible external state, ambiguous synthesis, and results that are expensive to verify.

Inspect the current host tool schema before relying on a concrete model name. If the configured model is unavailable, explain the constraint and use the configured fallback behavior.

Use native internal subagents rather than user-owned chats when the host distinguishes them. See [references/providers.md](references/providers.md) for capability mappings.

Parallelize only tasks with satisfied dependencies and disjoint mutable resources. Treat branches, databases, APIs, cloud resources, deployment slots, and shared documents as resources, not only files.

Pause new dispatch when the configured number of returned tasks awaits acceptance. A stale task does not consume review budget but keeps its owned resources locked until reconciled.

## 7. Accept through a narrow evidence aperture

Read [references/qa-checklist.md](references/qa-checklist.md) for the task-type acceptance surface.

Require a compact evidence packet. Keep full logs, reports, and diffs in files or tool state and return pointers rather than pasting them into the main conversation.

For each result:

1. read the concise result;
2. inspect the canonical artifact and the smallest evidence slice that proves each acceptance check;
3. widen inspection for high-risk work or inconsistent evidence;
4. write the verdict, evidence pointers, residual risk, and rework into the Acceptance Ledger;
5. carry only that checkpoint into later dispatch unless a regression or dispute requires reopening the raw evidence.

If evidence is missing, issue a bounded evidence follow-up. If acceptance requires a user scope, permission, or business decision, move the task to `waiting_for_context` and ask the specific question.

## 8. Recover and handle failures

Use these main states:

`draft -> ready -> in_progress -> review -> accepted`

Use these side states:

`waiting_for_context`, `blocked`, `stale`, `superseded`, `failed`

If a task misses its timeout or check-in without new evidence, mark it `stale`. Before stopping, taking over, or reassigning it, inspect the agent state, workspace, Git diff, and external resources so two agents do not repeat the same mutation.

After compaction, a new session, or a coordinator handoff, recover in this order:

1. objective and done definition;
2. current control state;
3. unaccepted tasks and latest acceptance entries;
4. actual Git, workspace, and external state;
5. only the sources required by the current critical path.

Do not replay the entire conversation to recover the task.

## 9. Close the task

Finish only when:

- every required task is accepted or has a user-approved disposition;
- artifacts live with their canonical owner;
- the main Agent performs an integrated acceptance pass;
- required Git, deployment, or external state is closed;
- the execution document points to results, evidence, residual risks, and unresolved facts;
- the user can quickly locate the result.

Update the execution document before the final response. Report the outcome, important evidence, remaining risks, and where the durable execution record lives.

## Evolution

Use user corrections, rework, orphaned tasks, review overload, resource conflicts, recovery failures, and model-cost mismatches as feedback.

Promote a rule only when the user explicitly generalizes it, the same behavioral failure recurs across tasks, one failure is high-risk with a clear regression check, or a real long task proves a reusable recovery pattern. Agent self-assessment is weak evidence.

Keep project facts in the project execution document. Put stable control rules in this file, detailed task and acceptance rules in references, and objectively checkable failures in evals or QA. Merge or remove obsolete rules instead of only appending. Preserve Git rollback and never silently change user authority, external-write defaults, or final-acceptance responsibility.
