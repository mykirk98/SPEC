# Plan Guideline

> How to write a plan.

---

## Workflow

1. Human writes a plan draft and shares the file path with Claude
2. Claude reads the draft, refines the Steps to satisfy Writing Steps, and raises any gaps found
3. Claude and human refine the plan together
4. Human gives final approval to begin execution
5. Claude begins execution — per-step review from there on is governed by `plan-execution.md`

---

## Plan Structure

Plan files live under `plan/`, not the project root (e.g. `plan/plan01.md`).

Plan structure follows `.claude/template/plan-template.md`.

Keep the template's fixed labels and the `[Structural]`/`[Behavioral]` tags as-is.

---

## Writing Goal, Scope, and Open Questions

- **Goal**: what the plan achieves and why, in 1-2 sentences — don't restate the Steps in detail
- **Scope**: `In` lists touched files/directories at a glance, even if inferable from the Goal; `Out` lists only boundary decisions that aren't obvious from the Goal, not everything unrelated
- **Open Questions**: if something needs to be discussed with the human, or you have a better idea, leave it here; every question must be resolved before final approval — if none remain, leave the section empty

---

## Writing Steps

- Each step is a coherent unit of work that can be built and verified independently
- Steps must be ordered by dependency (earlier steps should not rely on later ones)
- Each step title should describe what's changing — new behavior for `[Behavioral]` steps, restructuring for `[Structural]` steps — not what code is being written
- Never mix structural and behavioral changes (see `tidy-first.md` for the definitions) in the same step — structural steps always come first
- Every step must include Acceptance Criteria — these define what tests need to pass for the step to be complete

```markdown
- [ ] Step 1: [Structural] Extract the discount calculation into a helper
  Acceptance Criteria:
  - All existing tests pass (no behavior change)

- [ ] Step 2: [Behavioral] Add a loyalty discount for repeat customers
  Acceptance Criteria:
  - A customer with 3 or more purchases gets 10% off
  - A new customer gets no discount
```