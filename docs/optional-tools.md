# Optional tools — use at your own risk

These tools are optional suggestions, not required steps or endorsed performance presets. No utility on this page was installed or tested in this cloud workspace. Features and compatibility vary by release. Download from the official project/vendor links below, review current documentation, and avoid repackaged downloads or bundled “optimization packs.”

**Use at your own risk:** system-tweaking tools can affect Windows features, updates, devices, or startup software. Record your original settings, back up important files, and create a restore point if System Protection is available. A restore point is not a full backup and does not guarantee every change can be undone. Change one item at a time and keep a way to reverse it.

## Windows configuration and startup tools

| Tool | Useful for | Limits and precautions |
| --- | --- | --- |
| [O&O ShutUp10++](https://www.oo-software.com/en/shutup10) | Reviewing Windows privacy-related settings in one place | A privacy utility, not an established Apex FPS/latency fix. Read each setting's description and use its restore-point/export facilities where available. Avoid applying an entire preset blindly; some changes can affect services and Windows functionality |
| [Winaero Tweaker](https://winaerotweaker.com/) | Windows interface and behavior customization | Many options have no gaming benefit. Record each changed option and its original value; use the relevant reset control to undo it. Avoid speculative timer, security, update, or system-behavior changes simply because they are available |
| [Microsoft Sysinternals Autoruns](https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns) | Investigating what starts automatically, including entries beyond Task Manager's Startup apps | Start with inspection. Use signature verification and hide Microsoft entries to reduce clutter, but neither a third-party entry nor an unsigned file is automatically unnecessary or malicious. Uncheck an understood, nonessential entry rather than deleting it; recheck it to restore it. Leave unknown drivers, services, security software, and anti-cheat components alone |

For ordinary startup cleanup, try **Task Manager → Startup apps** first. Disable only apps you recognize and do not need at sign-in. A high startup-impact label describes startup work, not proof that an app is lowering FPS during a match. Do not use several tweaking utilities to change the same setting; that makes rollback harder to track.

## Measure before you tweak

| Tool | Useful for | Practical guidance |
| --- | --- | --- |
| [CapFrameX](https://www.capframex.com/) | Capturing and comparing FPS, frame-time plots, and low-percentile results | Use consistent capture duration, scene, and version. It measures frame delivery; an FPS result is not click-to-photon latency. Start with capture only, without extra overlay features |
| [Intel PresentMon](https://github.com/GameTechDev/PresentMon) | Frame presentation and supported performance telemetry across GPU vendors | An alternative to CapFrameX, not another recorder you need to run simultaneously. Available metrics depend on the system; label measured latency fields accurately |
| [HWiNFO](https://www.hwinfo.com/) | Checking temperatures, clock speeds, power limits, and memory readings | Sensors-only mode can help identify throttling. Avoid unnecessarily rapid polling; monitoring itself can add overhead. Keep the same monitoring setup for both comparison runs |
| [Microsoft Process Explorer](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer) | Investigating processes and unexpected background CPU activity | Inspect before acting. Do not terminate unfamiliar system or anti-cheat processes or force game priority as a blanket optimization |
| [LatencyMon](https://www.resplendence.com/latencymon) | Investigating driver/DPC/ISR behavior when audio dropouts or system-wide hitches occur | It evaluates real-time audio-related scheduling behavior, not mouse input latency or Apex responsiveness. A warning or named driver is a diagnostic lead, not proof of the cause; do not remove drivers solely on that result |

Start with Apex's performance display and Windows Task Manager. Add one capture tool and, only if needed, sensor logging. Do not install every tool in this table. Check current game and tool compatibility before using overlays; if a tool is blocked, do not attempt to bypass the restriction.

## A repeatable workflow

1. Capture a baseline using the [validation guide](validation.md), including your current cap, resolution, temperatures, and background apps.
2. Identify a specific problem: recurring frame-time spikes, high temperatures, background CPU work, or unwanted Windows behavior.
3. Choose the relevant tool and inspect first. Write down one proposed change and how to undo it.
4. Make that one change. Restart if required and repeat the same capture after warming shaders.
5. Keep the change only if it produces a repeatable benefit or an intentional privacy/customization preference. Revert regressions and changes with no useful result.

Privacy preferences can be worthwhile without affecting FPS. Keep that reason separate from a performance claim. Avoid registry cleaners, automatic driver-updater bundles, RAM cleaners, and one-click service-disabling scripts as routine gaming maintenance.

For Windows Fast Startup, BIOS Fast Boot, and simpler checks, see [Windows troubleshooting](windows-troubleshooting.md).
