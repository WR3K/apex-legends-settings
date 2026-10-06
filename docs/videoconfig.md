# Video configuration

Prefer the in-game menu: it generates settings appropriate to the current client. The root [videoconfig.txt](../videoconfig.txt) is an optional **merge fragment**, not a complete replacement or an executable autoexec.

1. Apply [in-game settings](../ingame.md), exit Apex, and back up `%USERPROFILE%\Saved Games\Respawn\Apex\local\videoconfig.txt`. Use the actual Windows Saved Games location if it has been relocated.
2. Open the existing file. For each key in our fragment that already exists, edit its value inside the existing `VideoConfig` block. Do not add a second block or duplicate keys. If a key is absent, leave it out and use the corresponding menu control.
3. Preserve all other values, particularly resolution, display mode, refresh rate if present, `setting.stream_memory`, and `setting.configversion`.
4. Leave the file writable during initial setup and testing. Launch Apex, check the menu, play a short test, exit, and inspect what the client saved. A reverted value may indicate a renamed or unsupported setting; read-only cannot make an unsupported setting work.

| Key | Intended setting |
| --- | --- |
| `setting.mat_vsync_mode` | In-game V-Sync disabled; driver V-Sync depends on the selected profile |
| `setting.mat_antialias_mode` | Anti-aliasing disabled |
| `setting.volumetric_lighting` | Volumetric lighting disabled |
| `setting.particle_cpu_level` | Low effects detail |

These mappings come from the reference config and require a current-client check. The fragment deliberately omits upstream's fixed 2560×1440 resolution, texture allocation, config version, and undocumented shadow overrides. ADS DoF belongs in the autoexec, not this fragment.

## Optional read-only after testing

See the [beginner walkthrough](beginners.md) for right-click → Properties → Read-only instructions and how to remove the attribute. Read-only can protect saved values from ordinary writes, but pressing Apply in game can still change the live session and supersede overlapping autoexec settings. It does not lock every `.cfg` or automatically re-run autoexec. Fully restart and verify which values actually reload. Leave it writable when troubleshooting or allowing a client update to migrate the file.
