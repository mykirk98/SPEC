# Git Workflow

> Conventions for landing a change on `project/fassto_main`.

---

## Branching

- Branch off the latest `project/fassto_main`; never commit directly to `project/fassto_main`
- Name branches `<type>/<kebab-description>`, reusing the types from `commit-convention.md` — e.g. `feat/loyalty-discount`, `fix/null-frame-crash`
- One logical change per branch; keep branches short-lived
- Rebase onto `project/fassto_main` to stay current rather than merging `project/fassto_main` in

---

## Pull / Merge Requests

- Open a pull/merge request (a PR on GitHub, an MR on GitLab) for every change that lands on `project/fassto_main`
- Its title follows the commit subject format `<type>(<scope>): <subject>`
- Its description explains why the change was made and links related issues (`Closes #123`)
- Keep each one small enough to review in one pass; split large work into separate requests
- Merge only when CI passes

---

## Merging

- Squash or rebase so `project/fassto_main` keeps a linear history — no merge commits for feature branches
- Delete the branch after it is merged
