# Plan

## Approach

Add a shared reasoning-effort type to the Copilot payload, model Anthropic's
`output_config.effort`, and translate explicit effort before falling back to
legacy `thinking.budget_tokens` buckets. Keep the field absent when neither
control is provided.

## Work Items

1. Extend request types for all Copilot-supported reasoning effort values.
2. Translate named effort and legacy thinking budgets with explicit precedence.
3. Add table-driven coverage for named values, budget boundaries, precedence,
   and unchanged requests.
4. Run the repository test, lint, typecheck, and build commands.

## Key Decisions

- Explicit `output_config.effort` wins over the inferred legacy budget.
- Legacy budgets map to `low` through `max`; Claude Code's `31999` maximum
  budget maps to `max`.
- Requests without an effort signal do not gain a default.
