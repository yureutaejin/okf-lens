# okf-lens project instructions

This file is the canonical source for project-wide instructions that every
agent must follow.

## Agent configuration is APM-owned

**All agent configuration must originate in `.apm/` and `apm.yml`.** This
includes skills, scoped rules, instructions, MCP servers, agent definitions,
prompts, hooks, and their installation configuration.

`apm install` deploys the project-managed Claude configuration here:

```text
.claude/
├── rules/   # APM-installed scoped instructions
└── skills/  # APM-installed Agent Skills
```

Read the applicable files in these directories as installed agent guidance.
Do not treat `.claude/` as an authoring location; change the APM sources and
run `apm install` to update its contents.
