# IYEN Agent Instructions

## Identity and scope

- Default GitHub organization: `IYENTeam`.
- Maintainer email for this repository: `iyen.team@gmail.com`.
- Work in the current checkout and preserve unrelated user changes.
- A GitHub URL grants read access only. Push, comment, close, merge, release, publish, deploy, or other external mutations require an explicit request.

## Working style

- Read relevant docs and skills before changing code.
- Prefer evidence from current source, tests, and official documentation over assumptions or stale comments.
- Fix root causes at the correct ownership boundary; add regression coverage when appropriate.
- Keep changes focused and reviewable. Use Conventional Commits.
- Update documentation when behavior or workflows change.

## Git and GitHub

- Start with `git status --short --branch` and preserve unknown work.
- Never use destructive Git commands or overwrite unique work without explicit approval.
- Use `gh ... --json` with narrow fields for GitHub reads.
- Do not use tight CI polling loops; follow one exact run and reuse fetched logs.
- Before reporting a remote task complete, verify the remote commit, PR, issue, workflow, or release state.
- Preserve contributor credit when modifying or landing external contributions.

## Skills and tools

- Skills live in `skills/<name>/SKILL.md` with `name` and `description` front matter.
- Run `npm run docs:list` when documentation may apply.
- Run `npm run skills:validate` after skill changes.
- Run `npm test` before committing or pushing changes to this toolkit.
- Use `github-deep-review` for non-trivial GitHub issues and PRs.
- Use `skill-cleaner` to diagnose duplicates and prompt-budget pressure; never delete from its report without an explicit cleanup request.

## Communication

- Respond in Korean by default and match the user's language when they switch.
- Lead with the outcome, then give proof, risk, and the next useful action.
- Never expose secrets, private user data, or confidential identifiers in output or public GitHub content.

