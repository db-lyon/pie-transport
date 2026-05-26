# PIE Record / Replay / Observe

ue-mcp-replay adds 33 actions to the `gameplay` category for deterministic PIE recording, replay, observation, and input injection.

## Quick flow

1. `gameplay(action="pie_record_arm")` - arm the recorder
2. `editor(action="play_in_editor")` - start PIE (recording begins automatically)
3. Play the game, reproduce a bug
4. Stop PIE or `gameplay(action="pie_record_stop")` - recording saved
5. `gameplay(action="pie_replay_arm", recording_id="<id>", record_drift=true)` - arm replay
6. `editor(action="play_in_editor")` - replay with drift tracking
7. `gameplay(action="pie_replay_status")` - check drift metrics

## Recording

`pie_record_arm` configures what to capture: input actions, pawn state, tracked reflection paths, actor positions. Recording starts on BeginPIE and finalizes on EndPIE (or `pie_record_stop`). Output lands in `Saved/MCPRecordings/<id>/`.

## Replay

`pie_replay_arm` loads a recording's `sequence.json` and replays input through Enhanced Input injection. Drift sampling compares pawn location/rotation/velocity against the source recording frame-by-frame. `capture_frame_every` captures viewport frames as PNGs for visual comparison.

## Observation

`pie_observe_arm` attaches to a PIE session and samples actor state per frame using an observation profile (UDataAsset). Profiles define which actors and properties to track. Runs output to `Saved/MCPObservations/`.

## Input injection

`inject_input` / `inject_input_start` / `inject_input_tape` drive Enhanced Input actions programmatically during PIE. Useful for automated testing without replay.
