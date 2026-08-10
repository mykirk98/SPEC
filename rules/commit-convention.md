# Git Commit Convention

> How to format commit messages and when to commit.

---

## Format

```
<type>(<scope>): <subject>

[body]

[footer]
```

---

## Type (required)

- `feat` — a new feature
- `fix` — a bug fix
- `docs` — documentation changes only
- `style` — formatting, whitespace (no logic change)
- `refactor` — code restructuring with no feature or bug change
- `test` — adding or updating tests
- `chore` — build process, dependency updates, tooling
- `perf` — performance improvements
- `ci` — CI/CD configuration changes
- `revert` — reverting a previous commit

- If a commit spans multiple types, classify by outward-observable effect: `feat`/`fix` > `perf` > `refactor` > `style`

---

## Scope (required)

- the module, component, or area affected

---

## Subject (required)

- Use the **imperative mood**: `add`, `fix`, `update` — not `added`, `fixes`, `updated`
- Keep it under **50 characters**
- Do **not** end with a period
- Be specific and descriptive

---

## Body (optional)

- Separate from the subject with a **blank line**
- Explain **why** the change was made, not what was changed
- Write each paragraph as a single line — no manual line breaks (e.g. 72-char wrap)
- Keep it under **300 characters**
- Do not mention co-authored by AI

---

## Footer (optional)

### Issue References

| Keyword | Effect |
|---------|--------|
| `Closes #123` | Auto-closes the issue on merge |
| `Fixes #123` | Same as Closes, used for bug fixes |
| `Refs #123` | Links without closing |

### Breaking Changes

- Append `!` right before the colon (after the scope, if present)
- Or include `BREAKING CHANGE:` in the footer

---

## Commit Practices

- Keep unrelated changes in separate commits
- Only commit when all tests, the formatter, and the linter pass cleanly — run the tools specified in the relevant `*-code-style.md`
- Prefer small, frequent commits over large, infrequent ones