# Agent Scripts

Shared agent instructions, skills, and small portable helpers for local workspaces.

This repo is the canonical place for:
- `AGENTS.MD`: shared hard rules for Codex/Claude-style agents
- `skills/`: reusable workflow skills, including repo-owned skills exposed by symlink
- `scripts/`: dependency-light helpers used across projects
- `hooks/`: local guardrails such as skill validation

## Path Placeholders

Values written as `<...>` are placeholders, not literal commands or directory names. Replace each one with the matching path or name for your own machine before using the examples.

For example:

```text
<AGENT_SCRIPTS_PATH> = /path/to/your/agent-scripts
<CODEX_SKILLS_PATH> = /path/to/your/.codex/skills
<CLAUDE_SKILLS_PATH> = /path/to/your/.claude/skills
<SECONDARY_SKILLS_PATH> = /path/to/your/secondary/skills
```

The actual locations are up to you. Absolute paths are the clearest choice; home-relative paths such as `~/your/path` also work when the command or tool expands `~`.

Other placeholders such as `<BUNDLE_NAME>`, `<SKILL_NAME>`, and `<REPO_OWNED_SKILLS>` should likewise be replaced with names or values from your own setup. Do not include the angle brackets after replacing a value.

## Skills

Skills are the main routing layer. Each `skills/<name>/SKILL.md` has YAML front matter:

```yaml
---
name: skill-name
description: "Short generic trigger phrase."
---
```

Rules:
- Keep descriptions short and generic; optimize for routing, not documentation.
- Keep skill bodies terse and operational.
- Prefer helper scripts under `skills/<name>/scripts/` when a workflow has repeatable commands.
- Validate after edits: `scripts/validate-skills`.
- Quote `description` in front matter.

Global discovery is built by `scripts/sync-skills` (idempotent; run on every machine after cloning or adding skills):
- Codex scans nested dirs, so it gets whole-root links: `<CODEX_SKILLS_PATH>/<BUNDLE_NAME> -> <AGENT_SCRIPTS_PATH>/skills`, `<CODEX_SKILLS_PATH>/<SECONDARY_NAME> -> <SECONDARY_SKILLS_PATH>`.
- Claude Code loads only `<CLAUDE_SKILLS_PATH>/<name>/SKILL.md` (exactly one level deep; per-entry symlinks are followed, category subfolders are not scanned). It gets a flat per-skill link mirror covering configured repos plus machine-local Codex skill extras.
- Name collisions resolve `<PRIMARY_SKILLS> > <SECONDARY_SKILLS> > codex-local`; the script prints skipped duplicates and prunes broken or stale managed links.

Shared skills live as real folders in `skills/`. Public shared skills may live in `<PUBLIC_SKILLS_PATH>` and be exposed here with tracked relative symlinks. Repo-owned skills stay canonical in their repo and are exposed here the same way, for example:

```text
skills/<SKILL_NAME> -> <PUBLIC_SKILL_TARGET>
skills/<REPO_SKILL_NAME> -> <REPO_SKILL_TARGET>
```

Add current symlinked repo-owned skills here:

```text
<REPO_OWNED_SKILLS>
```

## Agent Instructions

Shared hard rules live in `AGENTS.MD`.

Global setup (also maintained by `scripts/sync-skills`):
- `<CODEX_AGENTS_PATH> -> <AGENT_SCRIPTS_PATH>/AGENTS.MD`
- `<CLAUDE_INSTRUCTIONS_PATH> -> <AGENT_SCRIPTS_PATH>/AGENTS.MD`
- `<CLAUDE_AGENTS_PATH> -> <AGENT_SCRIPTS_PATH>/AGENTS.MD`

Downstream repos should use a pointer-style `AGENTS.MD`:

```text
READ <AGENT_SCRIPTS_PATH>/AGENTS.MD BEFORE ANYTHING (skip if missing).
```

Repo-specific rules go below that pointer. Do not copy the shared blocks into downstream repos.

## Helpers

`scripts/committer`
- Stages exactly the listed files.
- Enforces a non-empty commit message.
- Runs skill validation before committing.

`scripts/sync-skills`
- Builds the per-machine skill mirror: Codex whole-root links, Claude flat per-skill links, shared `AGENTS.MD` pointers.
- Idempotent; prints changes only, prunes broken or stale managed links, never clobbers real files.

`scripts/validate-skills`
- Checks every `skills/*/SKILL.md`.
- Verifies YAML front matter plus required `name` and `description`.
- Enable as a local hook with `git config core.hooksPath hooks`.

`scripts/docs-list.ts`
- Walks `docs/`.
- Enforces `summary` and `read_when` front matter.
- Prints onboarding summaries for repos that wire it in.

`scripts/browser-tools.ts`
- Standalone Chrome DevTools helper.
- Common commands: `start --profile`, `nav <url>`, `eval '<js>'`, `screenshot`, `console`, `network`, `search --content "<query>"`, `content <url>`, `inspect`, `kill --all --force`.
- Build optional binary with `bun build scripts/browser-tools.ts --compile --target bun --outfile <BROWSER_TOOLS_OUTPUT_PATH>`.

## Syncing

Treat this repo as canonical for shared agent rules and portable helper scripts.

When syncing downstream repos:
- Pull latest here first.
- Ensure each target repo starts with the pointer-style `AGENTS.MD`.
- Preserve repo-local rules below the pointer.
- Copy helper changes both directions only when the helper is meant to stay byte-identical.
- Keep scripts dependency-free and portable; no repo-specific imports or path aliases.

For submodules, repeat the pointer check inside each subrepo, push those changes, then bump submodule SHAs in the parent repo.
