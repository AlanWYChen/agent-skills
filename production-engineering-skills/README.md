# Production Engineering Skills Pack

This skill pack is organized by application domain:

```text
production-engineering-skills/
├── SKILL.md
├── web/
├── mobile/
├── backend/
└── shared/
    └── dependabot-policy/
```

Each domain contains its own production guidance. Shared repository workflows live in `shared/`; Dependabot policy has one authoritative copy used by every domain.

Notable additions:
- Web/mobile/backend-specific authentication guidance
- Google and Apple identity references
- OAuth/PKCE and passkey references
- testing split by test type
- GitHub Actions-first CI/CD guidance
- domain-specific production audits
- duplicated security/observability guidance customized to each domain

## Agent portability

The skills use the open [Agent Skills format](https://agentskills.io/specification):
YAML `name` and `description` metadata in each `SKILL.md`, Markdown instructions,
and relative links to supporting files. No model provider configuration, provider
SDK, or provider-specific tool names are required.

Install or copy the entire `production-engineering-skills/` folder into the skill
location supported by your agent. Use the top-level `SKILL.md` as the entry point;
it routes to the domain files and their supporting skills. Keep the directory
structure intact so relative links continue to work, including
`shared/dependabot-policy/` and its `assets/` directory. Domain CI/CD guides link
to that shared policy when Dependabot work is needed.

Discovery paths, invocation syntax, and nested-skill discovery vary by agent.
If automatic discovery is unavailable, ask your agent to read the top-level
`SKILL.md` directly. Nested skills with shared folder names, such as `testing`,
are distinguished by their domain paths; use those paths when selecting them
directly rather than relying on a bare name.

Use the tools available in the target environment to carry out the instructions.
GitHub Actions, Dependabot, Apple/Google identity, and framework references describe
the software being worked on; they do not require a particular AI provider.
