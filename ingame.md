# In-game baseline

Apply settings exposed by your current client. Names and available controls can change between releases. Start with native resolution; lower it only if GPU performance is limiting your target FPS.

| Setting | Starting point | Tradeoff or check |
| --- | --- | --- |
| Display mode | Fullscreen | Compare borderless if needed; measure on your system |
| Aspect ratio / resolution | Native | Reduced resolution helps mainly when GPU limited |
| FOV | Keep your accustomed value | Higher FOV can increase rendering load; 110 is not mandatory |
| FOV ability scaling | Disabled | Stable perceived zoom |
| Sprint view shake | Minimal | Less camera movement |
| V-Sync | Disabled in game | See driver profiles for tear-free play |
| NVIDIA Reflex | Enabled, if supported | Compare Enabled + Boost; extra power/heat may not improve results |
| Adaptive resolution FPS target | 0 | Consistent resolution; dynamic resolution is an optional GPU-limited tradeoff |
| Adaptive supersampling | Disabled | Avoid extra rendering load |
| Anti-aliasing | None initially | TSAA may look smoother but softer; compare motion clarity |
| Texture streaming budget | Start modestly within available VRAM | Increase for clarity if memory headroom permits; do not blindly choose None |
| Texture filtering | Bilinear initially | Compare 4×/8× for sharper surfaces and measured cost |
| Ambient occlusion | Disabled | Less shading cost |
| Sun shadow coverage / detail | Low | Lower shadow cost |
| Spot shadow detail | Disabled | Lower shadow cost |
| Volumetric lighting | Disabled | Lower lighting cost |
| Dynamic spot shadows | Disabled | Lower shadow cost |
| Model / map / effects detail | Low, where available | Compare clarity and frame times |
| Impact marks | Disabled | Less persistent clutter |
| Ragdolls | Low | Less physics/detail work |

Keep sensitivity, ADS multipliers, keybinds, audio channels, and gameplay preferences personal. Start with 1000 Hz mouse polling if supported; higher rates can increase CPU load. Mouse polling does not prescribe a texture streaming budget. Use the game's performance display to monitor FPS and network behavior, but do not equate ping with input latency.

The autoexec requests `hud_setting_adsDof "0"`. Compare ADS screenshots using the same weapon, optic, distance, and scene after a restart. It is a best-effort blur preference, not proof of lower latency; some optics and post-processing may remain unchanged.

For hardware-specific starting points and how to check RAM versus VRAM, see [choosing settings for your PC](docs/hardware-guide.md). For beginner file-editing and read-only behavior, see the [walkthrough](docs/beginners.md).
