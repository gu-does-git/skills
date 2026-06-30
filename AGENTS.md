# AGENTS.md — Skills Repo

## Identity

A public collection of [Agent Skills](https://agentskills.io/) — reusable skill modules that teach AI agents how to work with specific tools, libraries, and frameworks.

Each skill lives in `skills/<name>/` with a `SKILL.md` following the [Agent Skills specification](https://agentskills.io/specification.md).

## Skills

```
skills/
├── lodash/              SKILL.md + references/
├── momentjs/            SKILL.md + references/
├── bootstrap3/          SKILL.md + references/
├── fontawesome4/        SKILL.md + references/
├── angular-ui/          SKILL.md + references/
├── service-portal/      SKILL.md + references/
└── sn-sync-widget/      SKILL.md
```

### SKILL.md Format

Every skill has YAML frontmatter followed by Markdown instructions:

```yaml
---
name: <dir-name>          # required, matches directory name
description: <text>       # required, when to use this skill
license: <identifier>     # recommended
metadata:                 # optional
  <key>: <value>
---
```

## Adding a Skill

1. Create `skills/<name>/SKILL.md` with valid frontmatter
2. Optionally add `references/` for supporting docs
3. The `name` field in frontmatter **must** match the directory name
4. Keep SKILL.md under 500 lines — move details to reference files

```bash
mkdir skills/my-skill
touch skills/my-skill/SKILL.md
```

## Commit Convention

All commits **MUST** follow [Conventional Commits](https://www.conventionalcommits.org/). Hooks auto-add devmoji and validate.

| Type     | Emoji | Usage                  |
|----------|-------|------------------------|
| `feat`   | ✨     | New skill or feature   |
| `fix`    | 🐛     | Bug fix                |
| `chore`  | 🛠     | Maintenance, tooling   |
| `docs`   | 📝     | Documentation          |
| `refactor` | ♻️   | Code restructuring     |
| `perf`   | ⚡     | Performance            |
| `test`   | ✅     | Tests                  |
| `style`  | 🎨     | Formatting             |
| `build`  | 📦     | Build system           |
| `ci`     | 👷     | CI config              |
| `revert` | ⏪     | Revert                 |

```
<emoji> <type>(<scope>?): <description>
```

### Enforcement

- `prepare-commit-msg` hook → devmoji adds emoji
- `commit-msg` hook → commitlint validates conventional format
- **Agents:** just `git commit -m "feat: message"` — hooks handle the rest

## Dev Setup

```bash
bun install     # install dev dependencies (husky, commitlint, devmoji)
bun fmt         # format with prettier
```

## Tooling

| Tool | Purpose |
|------|---------|
| Husky | Git hooks |
| commitlint | Conventional commit validation |
| devmoji | Automatic emoji in commits |
| Prettier | Code formatting |
