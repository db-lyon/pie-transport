# ue-mcp-replay

PIE record, replay, observe, and input injection for [ue-mcp](https://github.com/db-lyon/ue-mcp).

## Install

```bash
ue-mcp plugin install ue-mcp-replay
```

This installs the npm package, deploys the native C++ module to your project's `Plugins/` directory, and adds the plugin to your `ue-mcp.yml`. Rebuild the UE project before launching the editor.

## What it adds

33 actions injected into the `gameplay` category:

- **Recording** - `pie_record_arm`, `pie_record_stop`, `pie_record_status`, `pie_record_list`, `pie_record_read`, `pie_record_delete`, `pie_mark`
- **Replay** - `pie_replay_arm`, `pie_replay_stop`, `pie_replay_status` with drift tracking and viewport capture
- **Observation** - `pie_observe_arm`, `pie_observe_stop`, `pie_observe_status`, `pie_observe_list`, `pie_observe_read` with profile-based sampling
- **Input injection** - `inject_input`, `inject_input_start`, `inject_input_update`, `inject_input_stop`, `inject_input_tape`
- **Profiles** - `pie_profile_create`, `pie_profile_read`, `pie_profile_update`, `pie_profile_delete`, `pie_profile_list`
- **Diff / Snapshot** - `pie_record_diff`, `pie_snapshot`
- **PIE inspection** - `get_pie_anim_state`, `get_pie_anim_properties`, `get_pie_subsystem_state`

## Develop

```bash
npm install
npm run build
```

See [ue-mcp plugin docs](https://ue-mcp.com/docs/plugins/) for the full author contract.
