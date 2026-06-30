# AGENTS.md — Skills Monorepo

## Identity

This is the **skills** monorepo — a public collection of reusable skill modules. Each package under `packages/*` is self-contained and independently usable.

## Commit Convention

All commits **MUST** follow [Conventional Commits](https://www.conventionalcommits.org/) with [Devmoji](https://github.com/zaaack/devmoji) emoji.

| Type | Emoji | Usage |
|---|---|---|
| `feat` | ✨ | New skill or feature |
| `fix` | 🐛 | Bug fix |
| `chore` | 🛠 | Maintenance, tooling, deps |
| `docs` | 📝 | Documentation |
| `refactor` | ♻️ | Code restructuring |
| `perf` | ⚡ | Performance improvement |
| `test` | ✅ | Tests |
| `style` | 🎨 | Formatting, whitespace |
| `build` | 📦 | Build system |
| `ci` | 👷 | CI config |
| `revert` | ⏪ | Revert |

**Format:**
```
<emoji> <type>(<scope>): <description>
```

**Examples:**
```
✨ feat(skill-registry): add semantic search
🐛 fix(auth): handle token expiry edge case
📝 docs: update API references
```

### Enforcement

- `prepare-commit-msg` hook runs `devmoji` to add the emoji
- `commit-msg` hook runs `commitlint` to validate format
- Agents: just `git commit -m "feat: message"` — hooks handle the rest

## Workspace

- **Runtime:** Bun 1.3+
- **Package manager:** `bun` (lockfile: `bun.lock`)
- **Workspaces:** `packages/*`
- **Formatting:** Prettier (`bun fmt`)

## Repository Structure

```
skills/
├── packages/          # skill packages (one directory per skill)
│   └── <skill-name>/
│       ├── package.json
│       └── src/
├── .husky/            # git hooks (pre-commit, commit-msg, prepare-commit-msg)
├── AGENTS.md          # this file
├── commitlint.config.js
└── package.json       # root workspace config
```

## For Agents

- **Commit directly** with `git commit -m "<type>: <description>"` — hooks validate + add emoji
- **Install deps** with `bun add <pkg>` (workspace-aware)
- **Run tests** with `bun test` in a package or `bun test --filter <skill-name>`
- **Format** with `bun fmt` before committing
- **New skill** → `mkdir packages/<name>`, create `package.json` with `"private": false`, add to workspace
