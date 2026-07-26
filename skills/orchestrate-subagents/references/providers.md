# Host capability mapping

The Skill describes capabilities, not a mandatory provider.

## Codex-style hosts

- Use native collaboration subagents for internal work.
- Do not create user-owned threads when an internal subagent is intended.
- Inspect the dispatch schema before setting a model or reasoning effort.
- When model override requires a reduced context fork, send a self-contained task packet with minimal inherited context.

## Claude Code-style hosts

- Use the host's native subagent or agent-team capability when available.
- Map configured tiers to models the current account can actually access.
- Preserve the same task packet, resource ownership, evidence return, and main-Agent acceptance rules.

## Hosts without model selection

- Keep the configured tier as a task classification.
- Use the host default model.
- Inform the user that model-specific cost control is unavailable.
- Retain high-risk tasks with the main Agent.

## Hosts without subagents

Use the execution document, task graph, recovery order, and acceptance ledger as a single-Agent workflow. State clearly that execution is sequential and no delegated context isolation is occurring.
