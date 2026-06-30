---
name: sn-sync-widget
description: Sync widget files to ServiceNow via Agent API after edits. Triggers on: sp_widget, sp_ng_template, template.html, script.js, client_script.js, css.scss, link.js, widget folder, sync to ServiceNow, sync_now, sn-scriptsync sync, push to instance.
license: MIT
---

# sn-sync-widget

After editing widget files (`sp_widget` or `sp_ng_template`), sync changes to ServiceNow using the Agent API.

## Workflow

After creating or editing any widget file, **always** call `sync_now` before reporting completion.

### Steps

1. Identify the active instance folder (`pdspmaindev/` or `dev352851/`)
2. Send sync request via Agent API:

```json
{
  "id": "widget-sync",
  "command": "sync_now"
}
```

3. Wait for the response file in the `agent/responses/` directory
4. Clean up both request and response files
5. Confirm to the user that the widget was synced

### What gets synced

- **New widget** (no sys_id in `_map.json`): `sync_now` triggers artifact creation in ServiceNow
- **Existing widget**: `sync_now` pushes all pending file changes via `update_record_batch`
- Widgets are multi-file — the extension manages `_map.json` automatically

### Trigger conditions

This skill activates whenever you:
- Edit files inside `*/sp_widget/*` or `*/sp_ng_template/*` paths
- Are asked to sync, upload, or push widget changes to ServiceNow
- Complete a multi-file widget change (template + script + css)
