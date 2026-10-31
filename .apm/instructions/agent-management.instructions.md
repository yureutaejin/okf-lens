---
description: APM ownership rules for all agent instructions, skills, and MCP configuration.
applyTo: "**"
---

- Treat `apm.yml` and `.apm/` as the source of truth for this repository's agent configuration.
- Treat the root `CLAUDE.md` as the source of truth for project-wide guidance; it does not permit manually managing agent primitives outside APM.
- Do not manually create or edit files under `.claude/`; regenerate them with `apm install`.
- Declare every reusable skill in `.apm/skills/<skill-name>/SKILL.md`. Each skill must conform to the Agent Skills specification.
- Declare every MCP server in `apm.yml` under `dependencies.mcp`; do not add MCP servers directly to Claude or Codex configuration files.
- Put always-applicable project rules in `.apm/instructions/*.instructions.md`, with `description` and `applyTo` frontmatter.
- After changing agent primitives or dependencies, run the repository's APM verification commands before relying on generated output.
