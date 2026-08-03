# IYEN Agent Instructions

## Communication

- Lead with the outcome, then explain cause, change, proof, risk, and remaining work.
- Use natural prose; use lists only for genuinely enumerable information.
- Respond in Korean by default and follow the user's language when they switch.
- Never expose secrets, private data, internal identifiers, or confidential material.

## Core workflow

- Read repository instructions, relevant docs, and matching skills before editing.
- Prefer current source and executable proof over issue comments, assumptions, and stale behavior.
- Fix root causes at the ownership boundary. Use a bounded refactor when it makes the invariant clearer.
- Add regression coverage when appropriate. Update docs and changelog for user-visible behavior.
- Keep changes coherent and reviewable. Use the repository's package manager and established conventions.
- Check new dependencies for release health, maintenance activity, adoption, and migration risk.

## GitHub and review

- A pasted GitHub URL authorizes inspection, not mutation.
- Start with `git status --short --branch`. Report overlapping dirty work before mutation and preserve unrelated changes.
- Use `gh ... --json` with narrow fields. Prefer one search/list query over per-item API loops.
- For PRs, inspect metadata, discussion, diff, adjacent code, tests, and exact-head checks.
- Treat contributor patches as proposals. Repair or rewrite when a cleaner bounded solution exists while preserving credit.
- For regressions, identify provenance with bounded history when possible and say `unknown` rather than guessing.
- UI changes need sanitized before/after proof when practical. Never upload sensitive screenshots.
- Before commit, push, or landing, perform an independent review when available and resolve actionable findings.
- User-facing fixes and landed PRs normally need a changelog entry; contributor-authored entries should thank the contributor.

## CI and proof

- Identify one exact CI run after a push. Poll with increasing intervals and fetch failed logs once.
- Fix in-scope CI failures and continue until the requested terminal state or an exact blocker.
- Live proof is required when behavior crosses a real service, account, browser, device, OS, or provider boundary.
- Mocks, fixtures, docs, and CI supplement live proof; they do not replace it when the real boundary is available.
- If required access is unavailable, complete safe local work and ask only for the exact remaining access or waiver.

## Git safety

- Work in the current checkout. Do not create a worktree or change branches unless requested or authorized by the invoked workflow.
- Never use destructive Git commands or discard, overwrite, stash, reset, clean, or delete unknown work without explicit approval.
- Stage and commit only intended paths. Prefer Conventional Commits.
- Do not amend unless requested. Use `--force-with-lease`, never blind force-push, when rewriting an authorized remote branch.
- Push only when the user asks or the invoked workflow clearly includes it.
- After landing, return to the expected default branch, pull `--ff-only`, and verify a clean synchronized checkout.

## Releases

- `ship` means commit and push; it does not mean release or publish.
- Release, version bump, tag, registry publication, deployment, and GitHub Release require explicit authorization.
- Before release, verify candidate-specific blockers, clean checkout, exact-head CI, tests, live proof, changelog, version policy, and artifacts.
- After release, verify the real tag, GitHub Release, package metadata, artifacts, integrity, and install/update path.
- Open backlog is not automatically a release blocker; only candidate-scoped work and demonstrated candidate regressions block.

## Runtime and shell safety

- Query exact secret names only; never dump the environment or print credential values.
- Use approved secret managers and scoped credentials. Redact output.
- Avoid broad globs and unresolved variables for destructive targets.
- In zsh, do not use `status` as a variable and do not assume scalar word splitting.
- For public GitHub bodies containing shell syntax, backticks, variables, or user text, use an inspected body file rather than inline double-quoted arguments.

## Repository tools

- Run `npm run docs:list` when documentation may apply.
- Run `npm run skills:validate` after skill changes.
- Run `npm test` before committing or pushing this toolkit.
- Use `github-deep-review` for non-trivial issues and PRs.
- Use `skill-cleaner` to diagnose context cost and duplicates; do not delete solely from its report.

## Closeout

- Report exact tests and remote state, not merely intended commands.
- Include full clickable issue/PR URLs, commit state, meaningful CI failures or retries, residual risk, and exact blockers.
- Never call a local patch complete when the requested outcome was remote.

