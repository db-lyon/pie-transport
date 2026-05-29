# PIE Record / Replay / Observe

pie-studio provisions the `pie` category: 33 actions for deterministic PIE recording, replay, observation, diffing, snapshots, and input injection. Actions are unprefixed - the category is the namespace.

## Quick flow

1. `pie(action="record_arm")` - arm the recorder
2. `editor(action="play_in_editor")` - start PIE (recording begins automatically)
3. Play the game, reproduce a bug
4. Stop PIE or `pie(action="record_stop")` - recording saved
5. `pie(action="replay_arm", recording_id="<id>", record_drift=true)` - arm replay
6. `editor(action="play_in_editor")` - replay with drift tracking
7. `pie(action="replay_status")` - check drift metrics

## Recording

`record_arm` configures what to capture: input actions, pawn state, tracked reflection paths, actor positions. Recording starts on BeginPIE and finalizes on EndPIE (or `record_stop`). Output lands in `Saved/MCPRecordings/<id>/`.

## Replay

`replay_arm` loads a recording's `sequence.json` and replays input through Enhanced Input injection. Drift sampling compares pawn location/rotation/velocity against the source recording frame-by-frame. `capture_frame_every` captures viewport frames as PNGs for visual comparison.

## Observation

`observe_arm` attaches to a PIE session and samples actor state per frame using an observation profile (UDataAsset). Profiles define which actors and properties to track. Runs output to `Saved/MCPObservations/`.

## Input injection

`inject_input` / `inject_input_start` / `inject_input_tape` drive Enhanced Input actions programmatically during PIE. Useful for automated testing without replay.
