# Agent Skills

Provider-agnostic production engineering skills for web, mobile, and backend applications.
The skills use the open [Agent Skills format](https://agentskills.io/specification)
with Markdown instructions, standard skill metadata, and relative supporting-file links.

## Included pack

```text
production-engineering-skills/
├── SKILL.md
├── web/
├── mobile/
├── backend/
└── shared/
    └── dependabot-policy/
        ├── SKILL.md
        └── assets/
```

Start with [the production engineering skill](production-engineering-skills/SKILL.md).
It routes to the relevant domain and supporting guidance. Dependabot policy is
maintained once under `shared/` and linked from each domain's CI/CD skill.

## Install in a project

Clone this repository, then copy the complete `production-engineering-skills/`
folder into your agent's supported project skill directory. For agents that use
`.agents/skills/`, run from your project's root, replacing `/path/to/agent-skills`
with the location of your clone:

```sh
mkdir -p .agents/skills
cp -R /path/to/agent-skills/production-engineering-skills .agents/skills/
```

Keep the entire pack together to preserve relative links, shared policies, and
templates. When updating an existing installation, compare local customizations
before replacing the installed pack with the latest version from this repository.
Record the source commit when you need reproducible installations.

## Agent compatibility

No model provider configuration, SDK, or provider-specific invocation syntax is
required. Skill discovery locations and nested-skill discovery vary by agent.
If automatic discovery is unavailable, ask the agent to read the pack's
`SKILL.md` directly and follow its relative links.

Nested skills can share names such as `testing` across domains. Select them by
domain path when necessary. Only read the domain and supporting files relevant
to the current task.

GitHub Actions, Dependabot, Apple/Google identity, and framework-specific guidance
describe the target software and platforms, rather than the agent provider.
Individual workflows still require the appropriate tools and access for their task.

## Maintaining the library

Make reusable skill changes here, then update project installations from this
repository. Keep instructions in `SKILL.md`, detailed guidance in linked files,
and reusable templates in `assets/`. Preserve relative links and validate skill
metadata and file references after reorganizing the pack.
