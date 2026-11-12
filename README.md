# Agent Skills

Provider-agnostic engineering skills for production applications and disciplined test-driven development.
The skills use the open [Agent Skills format](https://agentskills.io/specification)
with Markdown instructions, standard skill metadata, and relative supporting-file links.

## Included skills

```text
test-driven-development/
└── SKILL.md

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

[test-driven-development](test-driven-development/SKILL.md) is a standalone workflow
skill: derive tests from requirements first, verify a meaningful failing run, freeze
the tests, and only then implement — with separate test-author and implementer roles
in multi-agent work. The skill is advisory unless your agent's instruction file (for example `AGENTS.md`) requires loading it before implementation changes.

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
cp -R /path/to/agent-skills/test-driven-development .agents/skills/
```

Keep the entire pack together to preserve relative links, shared policies, and
templates. When updating an existing installation, compare local customizations
before replacing the installed pack with the latest version from this repository.
Record the source commit when you need reproducible installations.

## Agent compatibility

No model provider configuration, SDK, or provider-specific invocation syntax is
required. Skill discovery locations and nested-skill discovery vary by agent.
A client that scans only one directory level discovers the two top-level skills;
the support files and nested guidance are reached through relative links, so
install and preserve the whole tree. An optional tool-specific hint such as
`whenToUse` is ignored by clients that do not recognize it.
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
