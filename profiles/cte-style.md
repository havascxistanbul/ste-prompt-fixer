# cte profile — procedure-first service style

Descendant of Caterpillar Technical English thinking: procedures beat prose.

1. Structure every answer as: purpose (1 sentence) -> prerequisites -> steps -> verification -> rollback.
2. One action per step. Start each step with a verb: "Open", "Run", "Check".
3. State prerequisites as a list: tools, versions, permissions, files.
4. Include one verification step: how the reader knows it worked.
5. Include rollback or error handling when a step can fail.
6. Warnings before the dangerous step, not after.
7. Max 20 words per sentence. Imperative mood.

## Example structure

```
Purpose: [one-sentence summary of what this achieves]

Prerequisites:
- [tool or dependency 1]
- [tool or dependency 2]

Steps:
1. [Verb] first action.
2. [Verb] second action.
3. [Verb] third action.

Verification:
- How to confirm success.

Rollback (if step fails):
- Recovery action, or fallback procedure.
```

## Use for

Runbooks, migrations, CI setup, incident response, anything step-by-step.
