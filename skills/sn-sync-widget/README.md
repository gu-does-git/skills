# sn-sync-widget Skill

Syncs widget files to ServiceNow via the Agent API after edits. Handles new and existing widgets through `sync_now` commands.

## Contents

- **SKILL.md** — full skill with workflow, API format, and trigger conditions

## Workflow

1. Edit ServiceNow artifact files
2. Call `sync_now` via Agent API
3. Wait for response and clean up

## Source

MIT — custom tooling for ServiceNow widget development.
