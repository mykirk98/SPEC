# SPEC

> **S**oftware **P**lanning & **E**ngineering **C**onventions — a Claude Code rule set for plan-driven, disciplined development.
>
> Version 1.01

SPEC makes a coding agent work like an engineer instead of an autocomplete. Rather than letting it sprint through a vague request, SPEC enforces a loop: write a plan, execute one step, stop for review, log it, commit it. Around that loop sit the standards each step must meet — structural and behavioral changes kept apart, and a commit gate that requires green tests, formatter, and linter.

## What's inside

### `rules/` — loaded into every session

| File | What it governs |
| --- | --- |
| `plan-guideline.md` | Writing a plan: Goal, Scope, dependency-ordered Steps, Acceptance Criteria |
| `plan-execution.md` | Executing one: first unchecked step only, stop for human review, log, commit |
| `tdd-principles.md` *(optional)* | Red → Green → Refactor; a failing test before every fix |
| `tidy-first.md` | Structural vs behavioral changes — never mixed, structural first |
| `design-principles.md` | Cohesion, coupling, layering, and SOLID with violation signals |
| `commit-convention.md` | Conventional-commit format and the commit gate |
| `git-workflow.md` | Branching, pull requests, linear history |
| `logging-principles.md` | Levels, what to log, what never to log |
| `python-code-style.md` | Python conventions, enforced by ruff |
| `cpp-code-style.md` | C++ conventions, enforced by clang-format and clang-tidy |

`tdd-principles.md` is opt-in — delete it if you don't work test-first. The commit gate still requires the suite to pass; only the order changes.

### `template/` — starting points, not rules

| File | Destination | Purpose |
| --- | --- | --- |
| `plan-template.md` | `.claude/template/` | Skeleton for a plan |
| `plan-log-template.md` | `.claude/template/` | Skeleton for a per-step execution log |
| `pyproject.toml` | project root | ruff config backing `python-code-style.md` |
| `.clang-format` | project root | Microsoft style, 4-space indent |
| `.clang-tidy` | project root | Only the checks that map to a rule in the guide |

## Install

```bash
git clone https://github.com/mykirk98/SPEC.git

cp -r SPEC/rules     your-project/.claude/rules
cp -r SPEC/template  your-project/.claude/template
```

Then, in your project:

1. **Keep one language guide.** Delete the `*-code-style.md` you don't need — each is written to stand alone, so a Python project carries only the Python one.
2. **Wire up the tool configs.** Merge `[tool.ruff]` from `template/pyproject.toml` into your own `pyproject.toml`, and copy `.clang-format` / `.clang-tidy` to the project root. The rules name these tools; without the configs at the root, the commit gate has nothing to run.
3. **Create `plan/`.** Plans and their logs live there.

No `@import` or CLAUDE.md wiring is needed.

## Usage

SPEC runs on a plan file. Nothing happens until one exists.

1. **Draft the plan.** Copy `.claude/template/plan-template.md` to `plan/plan01.md` and fill in Goal, Scope, and a rough list of Steps.
2. **Hand it to Claude.** Give it the path. Claude refines the Steps against `plan-guideline.md` — dependency order, `[Structural]`/`[Behavioral]` tags, Acceptance Criteria — and leaves anything unresolved under Open Questions.
3. **Approve it.** Nothing is executed until you do.
4. **Say go.** Claude executes the first unchecked step only, marks it `[x]`, appends to `plan/plan01-log.md`, commits the code, and stops for your review.
5. **Repeat** until every step is checked off. The plan and its log are committed at the end, in one `docs` commit.

## Design decisions

**Tools enforce, prose explains.** Anything a formatter or linter can settle — line length, brace style, import order — is delegated to the tool and named once. The prose carries only what tooling cannot check: naming intent, layering, ownership, error-handling policy.

**Rules are always in context, so they stay short.** Every line in `rules/` costs tokens in every session. Duplicated guidance was merged, examples that only restated the prose were removed, and each rule has exactly one home that the others reference.

**The plan is the spine.** `plan-guideline.md` and `plan-execution.md` are only two of ten files, but they are the loop the rest plugs into — the commit convention runs at each step boundary, `tidy-first.md` decides how steps are split, and Acceptance Criteria define when a step is done.

## License

MIT — see [LICENSE](LICENSE).
