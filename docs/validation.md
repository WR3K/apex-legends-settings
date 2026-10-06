# Validate on your PC

Repository checks only establish file structure and documentation consistency. They cannot establish command support, FPS improvements, input latency, or anti-cheat compatibility in a running game.

## Confirm the config loads

Fully exit and relaunch Apex after editing an autoexec. The supplied Reddit discussion reports that runtime `exec` keybinds stopped working; neither a reload bind nor an `echo` line is a reliable execution check.

Temporarily enable an obvious cap such as `fps_max "60"` in autoexec and remove other manual caps. Restart and check the firing range, where your baseline must previously have exceeded 60 FPS. A 60 FPS ceiling is evidence that the file executed, not that every command works. Restore your chosen cap after the check. If the check fails, verify the real installation folder, filename extension, launch arguments, and competing limits.

Check ADS DoF separately using identical before/after scenes and full restarts. Keep an unmodified backup. If no visible difference occurs, report the setting as unverified/ineffective on that client rather than adding unrelated rendering overrides.

For capture and sensor utility suggestions, see [optional tools](optional-tools.md). Use one capture tool consistently rather than stacking monitoring utilities.

## Compare performance

1. Record CPU, GPU, RAM, driver and game versions, resolution, refresh rate, VRR status, cap, Reflex mode, and temperatures.
2. Warm up the game and shaders. Use the same firing-range route and actions for three 60–120 second captures per configuration, then check representative real matches. A range result alone cannot predict busy fights.
3. Change one group at a time: in-game graphics, cap/presentation, driver settings, then DoF. Keep background activity and recording tools consistent.
4. Record average FPS, 1% lows using the same tool/calculation, frame-time spikes, GPU utilization, VRAM use, and temperatures. Use an existing reputable frame-time capture tool if available; the game's counter alone cannot produce all these statistics.
5. Prefer repeatable improvements in busy-scene frame times to a single peak FPS number. Lower your cap if repeated fight drops produce poor pacing. Check tearing and aim feel too.

FPS is not a measurement of click-to-photon latency. Record PC latency only when supported telemetry is available, and label its scope; full end-to-end latency needs appropriate measurement equipment. Do not infer latency reductions from a config line alone.

| Date / game version | Profile / cap | Avg FPS | 1% low | Spikes / tearing | Latency method + result | Temperatures |
| --- | --- | --- | --- | --- | --- | --- |
| Pending on-PC test | Baseline | — | — | — | Unmeasured | — |
| Pending on-PC test | Candidate | — | — | — | Unmeasured | — |

## Roll back

Close the game. Restore your original autoexec, video config, and launch options from backup; if you had no autoexec before, remove the added file and its launch argument. Restore game and NVIDIA settings from your screenshots, or reset only the Apex driver profile if appropriate. Clear read-only on the video config if it was previously enabled. Restart and check the original behavior.
