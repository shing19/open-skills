# Setup and first-run configuration

## Configuration discovery

Look for configuration in this order:

1. `<project>/.agents/orchestrate-subagents.yaml`
2. the user's standard configuration directory under `orchestrate-subagents/config.yaml`
3. task-local settings in the execution document

Project configuration overrides user configuration. Never write a project configuration without the user's permission, because it may be committed.

## First run

If no configuration exists:

1. inspect whether the host supports internal subagents;
2. inspect whether model and reasoning-effort selection are available;
3. present detected capabilities rather than invented model names;
4. ask for low tier, medium tier, high-risk behavior, maximum concurrency, and review budget;
5. offer to save the result in a user-local config, or keep it task-local.

Ask the questions together when the interface allows it. Do not ask for values the host cannot use.

## Safe fallback

- If subagents are unavailable, explain that the Skill can only provide a documented single-Agent control loop.
- If model selection is unavailable, use the host default and tell the user that tier-specific cost control cannot be guaranteed.
- If a configured model is unavailable, follow `fallback.unavailable_model`; never silently choose a more expensive model.
- Keep high-risk work with the main Agent unless the user explicitly configured another behavior.

## Configuration privacy

Do not commit user-local model preferences, account identifiers, provider credentials, or machine paths. A repository may commit a project configuration only when its collaborators intentionally share those choices and no credentials are present.
