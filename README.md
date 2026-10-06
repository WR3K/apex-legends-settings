# Apex Legends settings

A performance-focused configuration for high FPS, low input latency, and consistent frame times. Inspired by [DominicKlmNL/apex-legends-config](https://github.com/DominicKlmNL/apex-legends-config), with ADS depth of field disabled as a personal preference.

This is a starting point, not a measured performance guarantee. Includes WR3K's Ryzen 7 5700X3D / RTX 3060 Ti / 32 GB RAM / 360 Hz example, currently capped at 170 FPS with G-SYNC off. Other PCs should choose their own targets. No commands have been validated in a running Apex client here; patches can ignore, clamp, or remove settings. Maximum FPS and the smoothest tear-free presentation can require different choices.

## New to configs?

Start with the [beginner walkthrough](docs/beginners.md) for finding both Apex folders, opening files in Notepad, saving `.cfg` files, and using read-only correctly. Then use the [hardware guide](docs/hardware-guide.md) to choose settings for your PC.

## Files

| File | Purpose |
| --- | --- |
| [Beginner walkthrough](docs/beginners.md) | Plain-language terms, files, Notepad, backups, and read-only |
| [Hardware guide](docs/hardware-guide.md) | Entry-level through high-end choices and WR3K's 170 FPS example |
| [Optional tools](docs/optional-tools.md) | System utilities, performance measurement, and use-at-your-own-risk guidance |
| [Windows troubleshooting](docs/windows-troubleshooting.md) | Practical checks and Fast Startup versus BIOS Fast Boot |
| [autoexec.cfg](autoexec.cfg) | Minimal config, including `hud_setting_adsDof "0"` |
| [Video config guide](docs/videoconfig.md) | Safely merge the [videoconfig.txt](videoconfig.txt) fragment |
| [In-game settings](ingame.md) | Graphics and input baseline |
| [NVIDIA settings](nvidia-settings.md) | Reflex, G-SYNC, driver settings, and FPS caps |
| [Steam launch options](launchoptions-steam.md) | Installation and launch arguments |
| [EA app launch options](launchoptions-ea-app.md) | Installation and launch arguments |
| [Validation](docs/validation.md) | Repeatable comparisons and rollback |
| [Sources and differences](docs/sources.md) | Attribution, evidence limits, and upstream changes |

## Install

1. Close Apex. Back up existing launch options, `<Apex install>/cfg/autoexec.cfg`, and `%USERPROFILE%\Saved Games\Respawn\Apex\local\videoconfig.txt`. Take screenshots of game and NVIDIA settings.
2. Choose a presentation profile in [NVIDIA settings](nvidia-settings.md). Apply the [in-game baseline](ingame.md) first and benchmark it before adding config overrides.
3. Review [autoexec.cfg](autoexec.cfg), merge it with your existing config if necessary, and place it in the game's `cfg` directory. Keep the filename `autoexec.cfg`, not `autoexec.cfg.txt`.
4. Add `+exec autoexec.cfg` in your launcher's launch arguments. See the Steam or EA guide above.
5. Optionally merge the video config fragment following its guide. **Do not replace your full game-generated video config with this fragment.** Preserve display, resolution, texture budget, and version fields.
6. Restart, verify settings and ADS appearance, then follow the validation guide. Keep only changes that improve your measurements or preferred appearance.

No installer, account credentials, build tools, or background services are required. The cloud workspace can edit and inspect these files; applying and measuring them requires your Windows Apex installation.

## License

The repository retains its existing [GPL-3.0 license](LICENSE). Upstream-derived settings are credited in [sources](docs/sources.md), with the upstream MIT notice preserved in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
