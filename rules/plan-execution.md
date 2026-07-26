# Plan Execution Guideline

> How Claude Code reads and executes `plan.md`.

---

## Execution Rules

### 1. One step at a time
- Execute only the **first unchecked** `- [ ]` item — never move on to the next until it is complete.

### 2. All completion criteria must be met
- If a step includes `Acceptance Criteria:`, every criterion must be met before the step is done.
- If no criteria are listed, use the step description itself as the standard.

### 3. Stop after completion
- When a step is done, update `- [ ]` to `- [x]`.
- **Stop immediately** and wait for human review — do not resume until approved.

### 4. Stay within scope
- Do not modify any file, module, or feature not mentioned in the step.
- Do not touch code that "seems like it could use improvement" if it is outside the step scope.
- If out-of-scope work appears necessary, report it to the human instead of acting on it.

### 5. Write a log entry after each step
- When a step is complete, append an entry to the log file before stopping.
- Log file: `<plan-filename>-log.md` next to the plan file (e.g. `plan/plan01.md` → `plan/plan01-log.md`); create it if absent.

Each log entry must follow the format in `.claude/template/plan-log-template.md`.

### 6. Commit after each step
- When a step is complete, commit the code changes following `commit-convention.md`.
- Do **not** include plan files (`plan/*.md`) in this commit.
- After **all** steps are complete, commit everything under `plan/` in a single `docs` commit.