---
name: small-committable-batches
description: Mandatory workflow for splitting any code or documentation change into small, self-contained batches that can each be committed and reviewed on their own. Use this skill for every task that writes or edits code, tests, config, READMEs, ADRs, runbooks, or any other docs, including new features, bug fixes, refactors, new pages, and doc rewrites. Apply it even when the user does not mention batches, commits, or reviews; skip it only for trivial one-line changes or pure questions that produce no edits.
---

# Small, Committable Batches

This is a hard requirement. Every change is delivered as a sequence of small batches, and each batch must be reviewable and committable on its own.

Large changes are hard to review: reviewers miss bugs, lose context, and cannot approve one part while asking for changes to another. Small batches keep each review to a few minutes and keep the project working at every step.

## Workflow

1. **Plan the batches first.** Before making any edit, split the task into an ordered list of batches and show the plan to the user. One line per batch: what it changes and how it will be verified.
2. **Do one batch.** Make only the changes that batch needs.
3. **Verify it.** The project must be in a working state after the batch: it builds, tests pass, docs render, and nothing points to anything that does not exist yet.
4. **Hand it off.** Summarize what changed, propose a commit message, and stop. Wait for the user to review before starting the next batch.
5. **Repeat** until the plan is done. If review feedback changes the plan, update the plan and show it again.

Do not commit unless the user explicitly asks. Each batch only needs to be ready to commit.

## What makes a good batch

- **One logical change.** A single concern a reviewer can understand in a few minutes.
- **Self-contained.** It does not depend on a later batch to compile, pass tests, or make sense.
- **Small.** If a batch touches many files or grows past a few hundred changed lines, split it further.
- **Not mixed.** Never combine unrelated concerns, for example refactor with feature, formatting with behavior change, or a doc rewrite with a new doc section.
- **Ordered.** Each batch builds on the previous one, for example prep or refactor, then the new capability, then tests, then docs.

## Code

- Put preparatory refactors in their own batch before the change that needs them, with behavior unchanged and tests passing.
- Keep a test with the code it covers when that keeps the batch small. Otherwise, add the tests in the next batch, as long as the project still builds and passes.
- Keep generated code, dependency bumps, and formatting-only changes in separate batches.

## Documentation

Documentation follows the same rules, but the unit is smaller:

- **One section per batch.** Add or rewrite at most one section in each batch.
- **Never write a whole page in one batch**, even for a brand-new document. Build pages up one section at a time.
- **New documents start with an outline.** The first batch contains only the title, a short intro, and the planned section headings. Each later batch fills in exactly one section.
- **Keep structure separate from content.** Moving, renaming, or reorganizing goes in its own batch, without content edits.

## Example plans

**Code: add retry support to an HTTP client**

```
1. Extract request sending into its own function (no behavior change) -> verify: existing tests pass
2. Add a retry option with default off -> verify: build + existing tests pass
3. Add unit tests for retry behavior -> verify: new tests pass
4. Document the retry option in the README "Configuration" section -> verify: docs render
```

**Documentation: write a new runbook**

```
1. Outline: title, intro, and headings for Overview, Alerts, Diagnosis, Remediation -> verify: renders
2. Fill in the Overview section -> verify: renders
3. Fill in the Alerts section -> verify: renders
4. Fill in the Diagnosis section -> verify: renders
5. Fill in the Remediation section -> verify: renders, links resolve
```

## When a task cannot be batched

If a change really cannot be split, for example an atomic rename that has to touch every caller at once, say so and explain why before you start. Keep that batch free of any other changes. Delivering one large, monolithic change without that explanation means this skill was not followed.
