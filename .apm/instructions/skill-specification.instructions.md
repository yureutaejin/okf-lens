---
description: Mandatory Agent Skills specification and directory requirements for every project skill.
applyTo: ".apm/skills/**"
---

- Every skill MUST conform to the Agent Skills specification at `https://agentskills.io/specification`.
- A skill MUST be a directory at `.apm/skills/<skill-name>/` containing, at minimum, the required entry file `SKILL.md`.
- `SKILL.md` MUST begin with YAML frontmatter and MUST include non-empty `name` and `description` fields.
- The frontmatter `name` MUST exactly match `<skill-name>`, be 1–64 characters, and use only lowercase letters, digits, and single hyphens. It must not start or end with a hyphen or contain consecutive hyphens.
- The `description` MUST state both what the skill does and when an agent should use it.
- Optional bundled resources belong directly under the skill directory: `scripts/` for executable helpers, `references/` for on-demand documentation, and `assets/` for static resources. Keep references from `SKILL.md` relative and one level deep.
- Do not create standalone skill files, place skills outside `.apm/skills/`, or bypass APM by copying a skill directly into `.claude/`, `.codex/`, or `.agents/`.
- Before installation, validate the directory name, frontmatter, and relative file references. After any change, regenerate managed output with the APM commands documented in the `agent-rules` skill.
