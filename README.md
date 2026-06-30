# Skills

A public collection of [Agent Skills](https://agentskills.io/) — reusable skill modules that teach AI agents how to work with specific tools, libraries, and frameworks.

## Skills

| Skill | Description |
|---|---|
| [lodash](skills/lodash/) | Lodash utility library — transforms, deep clone, debounce, chaining |
| [momentjs](skills/momentjs/) | Moment.js date/time parsing, formatting, manipulation, timezones |
| [bootstrap3](skills/bootstrap3/) | Bootstrap 3 grid, components, JS plugins, forms, responsive utilities |
| [fontawesome4](skills/fontawesome4/) | Font Awesome v4.7 icon library — 675+ icons |
| [angular-ui](skills/angular-ui/) | Angular-UI Bootstrap directives (ui.bootstrap) |
| [service-portal](skills/service-portal/) | ServiceNow Service Portal widgets, pages, portals, themes |
| [sn-sync-widget](skills/sn-sync-widget/) | Sync widget files to ServiceNow via Agent API |

## Format

Every skill follows the [Agent Skills specification](https://agentskills.io/specification.md):

```
skill-name/
├── SKILL.md          # Metadata + instructions (YAML frontmatter + Markdown)
├── references/       # Optional: reference documentation
└── scripts/          # Optional: executable scripts
```

## Usage

Skills are auto-detected by agents that support the format (Claude Code, VS Code, GitHub Copilot, Cursor, OpenCode, and [many others](https://agentskills.io/clients.md)). Clone the repo or point your agent at it.

```bash
git clone https://github.com/gu-does-git/skills.git
```

## Development

```bash
bun install          # install dev dependencies
```

Commit hooks enforce [Conventional Commits](https://www.conventionalcommits.org/) with devmoji:

```bash
git commit -m "feat: add new skill"
# → "✨ feat: add new skill"
```

See [AGENTS.md](AGENTS.md) for the full commit convention and workspace guide.

## License

MIT — see each skill's `SKILL.md` frontmatter for license details.
