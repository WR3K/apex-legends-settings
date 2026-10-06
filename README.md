# Apex Legends settings

A performance-focused configuration for high FPS, low input latency, and consistent frame times. Inspired by [DominicKlmNL/apex-legends-config](https://github.com/DominicKlmNL/apex-legends-config), with ADS depth of field disabled as a personal preference.

This is a starting point, not a measured performance guarantee. Includes example PC specifications: Ryzen 7 5700X3D, RTX 3060 Ti, 32 GB RAM, and a 360 Hz display, with an example 170 FPS cap and G-SYNC off. Other PCs should choose their own targets. The configuration commands have not been validated in a running Apex client for this guide; patches can ignore, clamp, or remove settings. Maximum FPS and the smoothest tear-free presentation can require different choices.

## Downloads

There are **four configuration files** below, plus this README and the project license. You do not need to install all four. `settings.cfg`, `profile.cfg`, and `videoconfig.txt` are **merge fragments**, not full replacement files. Back up your game-generated originals and edit only matching existing keys. Do not overwrite them with these downloads.

| File | Purpose | Exact destination | Raw file |
| --- | --- | --- | --- |
| [autoexec.cfg](autoexec.cfg) | Optional startup commands; current-client support unverified | `<Apex installation>\cfg\autoexec.cfg` | [Raw autoexec](https://raw.githubusercontent.com/WR3K/apex-legends-settings/main/autoexec.cfg) |
| [settings.cfg](settings.cfg) | Optional mouse-acceleration preference; preserve your binds and sensitivity | `%USERPROFILE%\Saved Games\Respawn\Apex\local\settings.cfg` | [Raw settings fragment](https://raw.githubusercontent.com/WR3K/apex-legends-settings/main/settings.cfg) |
| [videoconfig.txt](videoconfig.txt) | Graphics settings fragment; preserve resolution and VRAM budget | `%USERPROFILE%\Saved Games\Respawn\Apex\local\videoconfig.txt` | [Raw video fragment](https://raw.githubusercontent.com/WR3K/apex-legends-settings/main/videoconfig.txt) |
| [profile.cfg](profile.cfg) | ADS DoF preference; preserve other gameplay preferences | `%USERPROFILE%\Saved Games\Respawn\Apex\profile\profile.cfg` | [Raw profile fragment](https://raw.githubusercontent.com/WR3K/apex-legends-settings/main/profile.cfg) |

`<Apex installation>` means the folder opened by Steam's **Browse local files** or the EA app's install-location control; it is not text to paste into Windows Run. The Saved Games paths can be pasted into Run and may differ if you relocated Saved Games. The downloadable `profile.cfg` is an Apex preferences fragment, **not** an NVIDIA driver profile.

For download and Notepad instructions, start with the [beginner walkthrough](#beginners).

## Contents

- [Quick setup](#quick-setup)
- [Autoexec support and removal](#autoexec-status)
- [Settings and profile files](#saved-configs)
- [Beginner walkthrough](#beginners)
- [Choose settings for your PC](#hardware)
- [In-game settings](#in-game)
- [NVIDIA settings and frame pacing](#nvidia)
- [Video configuration](#video-config)
- [Steam launch options](#steam)
- [EA app launch options](#ea-app)
- [Validation and rollback](#validation)
- [Windows and PC troubleshooting](#windows)
- [Optional tools](#tools)
- [Screenshot checklist](#screenshots)
- [Sources and implementation notes](#sources)
- [Third-party notices](#third-party)
- [Project license](#project-license)

<a id="quick-setup"></a>

## Quick setup

1. Close Apex. Back up existing launch options and all original files you intend to edit from the [destination table](#downloads). Take screenshots of game and NVIDIA settings.
2. Choose a presentation profile in [NVIDIA settings](#nvidia). Apply the [in-game baseline](#in-game) first and benchmark it before adding config overrides.
3. If using the optional startup config, review [autoexec.cfg](autoexec.cfg), merge it with your existing config if necessary, and place it in the game's `cfg` directory. Keep the filename `autoexec.cfg`, not `autoexec.cfg.txt`.
4. Only if using autoexec, add `+exec autoexec.cfg` in your launcher's launch arguments. See the [Steam](#steam) or [EA app](#ea-app) instructions below.
5. Optionally merge the video config fragment following its guide. **Do not replace your full game-generated video config with this fragment.** Preserve display, resolution, texture budget, and version fields.
6. Optionally merge [settings.cfg](settings.cfg) and [profile.cfg](profile.cfg) following the [saved config instructions](#saved-configs).
7. Restart, verify settings and ADS appearance, then follow the validation guide. Keep only changes that improve your measurements or preferred appearance.

No installer, account credentials, build tools, or background services are required. Applying and measuring these settings requires your Windows Apex installation.

<a id="autoexec-status"></a>

## Autoexec support and removal

**Status as of 2026-10-07: startup autoexec support remains unverified for this guide, not confirmed removed.** The referenced community thread reports that mid-game `exec` reload binds stopped working. That does not establish that `+exec autoexec.cfg` at launch stopped working, and a file loading does not establish that every command inside it is accepted. The reference repository still documents startup loading; this is community evidence, not a current-game test.

Autoexec stays available as an **optional** file. Follow the [execution check](#validation) before relying on it. In-game controls already cover its active viewing preferences; autoexec is not necessary for the baseline. The ADS DoF preference now lives in the `profile.cfg` fragment, so it does not depend on autoexec executing.

If startup loading does not work on your installation after checking the folder, extension, and launch options:

1. Close Apex. Remove `+exec autoexec.cfg` from Steam/EA launch options; keep your chosen FPS cap. For the example 170 FPS setup, no-autoexec launch options are simply `+fps_max 170`.
2. Move an autoexec you installed from this repository into your backup folder. If you merged it with an existing autoexec, restore that original instead of deleting someone else's preferences.
3. Set FOV ability scaling and sprint view shake in the game menu. Apply the saved-file fragments only to matching keys that your game generated.
4. Restart and recheck. Record the game version and failed test rather than describing all autoexec support as removed on every client.

Do not add a runtime reload bind or an `exec` chain through profile/settings files as a workaround. Unsupported commands do not become supported when moved to another file.

[Back to contents](#contents)

<a id="saved-configs"></a>

## Settings and profile files

Launch Apex once, save your preferences in the menus, and exit normally so it can generate its own files. Close the game before editing them. Use **Windows + R**, paste the folder path below, and press Enter. For Notepad and filename help, see the [beginner walkthrough](#beginners).

| Open this folder | Find this file | What to do |
| --- | --- | --- |
| `%USERPROFILE%\Saved Games\Respawn\Apex\local` | `settings.cfg` | Back up the original. If `m_acceleration` already exists, optionally change its value to `"0"`. Leave binds, sensitivity, ADS multipliers, and all other lines intact |
| `%USERPROFILE%\Saved Games\Respawn\Apex\profile` | `profile.cfg` | Back up the original. If `hud_setting_adsDof` already exists, change its value to `"0"`, save, restart, and compare ADS appearance |

Edit the existing line instead of appending a duplicate. **Do not copy these short fragments over the full files.** Do not add `+exec settings.cfg` or `+exec profile.cfg`; they are game-managed saved preferences, not additional startup scripts. These paths and example key locations are documented in a historical community reference; verify against what your installed client generates.

If a file or key is missing, do not create a replacement from the downloadable fragment. Check the Windows account and relocated Saved Games folder (`shell:SavedGames`), then use the available in-game control. An absent ADS DoF key means this method is unverified for that installation; do not promise that pasting it elsewhere will work.

Keep settings/profile writable during testing and normally thereafter so binds and preferences can save. Read-only is optional file protection, not a performance setting, and can prevent permanent menu changes. See the [read-only explanation](#beginners). It is not required to apply these fragments.

Neither fragment sets your sensitivity, controller settings, resolution, or FPS cap. `m_acceleration "0"` is an optional input preference, not a proven latency improvement. Neither fragment's behavior has been verified in a running Apex client for this guide.

[Back to contents](#contents)

<a id="beginners"></a>

## Beginner walkthrough

You do not need to understand every setting to begin. Back up your files, make one change at a time, and test it. Use the in-game settings first; custom files are optional.

### What the terms mean

| Term | Plain meaning |
| --- | --- |
| FPS | Frames the game produces each second; higher is useful when frames arrive consistently |
| Hz | How often your monitor refreshes each second; a 360 Hz screen does not make the PC render 360 FPS |
| Frame time | Time taken to produce a frame; sudden spikes feel like stutter |
| FPS cap | A ceiling on frame production, such as `+fps_max 170`; it cannot guarantee the PC always reaches it |
| Latency | Delay between an action and its visible result; network ping is a separate contributor to online responsiveness |
| 1% low | A tool-dependent summary of the slowest frames; compare results using the same tool |
| VRAM / RAM | GPU memory for graphics / system memory; 32 GB RAM does not mean 32 GB VRAM |
| G-SYNC / FreeSync / VRR | Monitor refresh adapts to frame delivery within a supported range, reducing tearing |
| V-Sync | Controls frame presentation to prevent tearing; its latency tradeoff depends on the setup |
| Reflex | NVIDIA's supported in-game feature for reducing rendering-related latency |
| Autoexec / `.cfg` | A text file containing commands the game attempts to run at startup |
| Video config | The game's saved graphics settings, stored separately from its installed files |
| DoF / ADS | Depth of field (focus blur) / aiming down sights |

### Download this repository

On this repository's GitHub page, choose **Code → Download ZIP**. In File Explorer, right-click the downloaded ZIP → **Extract All**. Open the extracted folder. For a single file on GitHub, use its **Raw / Download raw file** control; saving the normal webpage can produce HTML instead of a config.

### Show filename extensions

Open File Explorer with **Windows + E**. On Windows 11 choose **View → Show → File name extensions**; on Windows 10 use **View → File name extensions**. This lets you distinguish `autoexec.cfg` from the incorrect `autoexec.cfg.txt`.

### Find the installed game files

**Steam:** Open Steam → **Library** → right-click **Apex Legends** → **Manage → Browse local files**. Alternatively use **Properties → Installed Files → Browse**. File Explorer opens the actual installation, even if you installed on a different drive. Open its **cfg** folder. This is where `autoexec.cfg` goes.

**EA app:** Open the Library, select Apex, and look for **Manage / View properties** and the installation location. Use **Browse** if offered, or open the displayed path in File Explorer. Labels vary by EA app version. Open the **cfg** folder inside that installation.

Do not guess a Steam drive letter or put the autoexec in the Windows Saved Games folder. If `cfg` is missing, first confirm you are in the folder containing the game's executable; create a folder named `cfg` there only if necessary.

### Find your saved video settings

1. Run Apex once, apply your preferred resolution, then close it normally.
2. Press **Windows + R** to open Run.
3. Paste the following path, including the percent signs, and press **Enter**:

```text
%USERPROFILE%\Saved Games\Respawn\Apex\local
```

4. Find `videoconfig.txt`. `%USERPROFILE%` expands to your Windows user folder; you do not need to type your username.
5. If the folder is missing, use **Windows + R → `shell:SavedGames`** and look for **Respawn → Apex → local**. Saved Games may have been relocated. Confirm you have launched Apex under this Windows account.

There are three destination folders: the install's `cfg` folder holds autoexec; Saved Games `local` holds settings/video config; Saved Games `profile` holds profile.cfg. See the [destination table](#downloads).

### Back up and open files in Notepad

1. Close Apex. Copy each original file to a separate backup folder, such as `Documents\Apex-settings-backup`. Keep a screenshot or text copy of your existing launch options too.
2. Right-click the file → **Open with → Notepad**. Windows 11 may show **Show more options**, **Edit in Notepad**, or **Choose another app** first.
3. Edit only the intended lines. Preserve quotation marks and braces. Lines beginning with `//` in the downloadable autoexec are comments; they do not execute.
4. Press **Ctrl + S**. If saving fails, check the file's read-only attribute using the next section; do not change folder permissions blindly.
5. To create a new autoexec in Notepad, choose **File → Save As**, set **Save as type: All files**, and enter `autoexec.cfg`. Use UTF-8, then verify the final filename in File Explorer.

If an autoexec already exists, merge the wanted lines instead of overwriting binds and personal preferences. For video settings, follow the [merge guide](#video-config): the repository's `videoconfig.txt` is deliberately incomplete and must not replace your full file.

### Optional: set or remove read-only

Leave the video config writable while choosing and testing settings. Once you have a known-good backup, read-only can help prevent ordinary writes to that file, but it is not required for this guide.

1. Close Apex and save the intended `videoconfig.txt` in Notepad.
2. In File Explorer, right-click **that file** → **Properties**.
3. On **General**, under **Attributes**, tick **Read-only**.
4. Click **Apply → OK**. To edit or save new permanent settings later, untick it and click **Apply → OK** first.

Use the file's checkbox, not the folder's checkbox. Do not mark the entire Apex folder read-only. An autoexec normally only needs to be read by the game; making it read-only is usually unnecessary.

#### What happens if you Apply graphics settings in game?

**Read-only protects the file on disk; it does not lock live settings in the running game.** Pressing Apply can change graphics for the current session even if those values cannot be written to the read-only video config. A menu change can also supersede an overlapping value previously set by autoexec. This does not mean the game edited the autoexec itself.

On a full restart, Apex normally loads its saved settings and attempts to execute your startup autoexec again. Unsupported commands, loading order, other writable settings files, or cloud synchronization can affect the result, so read-only is not a guarantee that every setting will return exactly as expected. It also cannot make an unsupported command work.

For a permanent change: close the game, remove read-only, edit the relevant file or apply settings in game, exit normally, inspect the saved values, and test another launch. Re-enable read-only only if you still want it. Remove read-only before troubleshooting resolution changes or letting a game update migrate the config schema.

Continue with [in-game settings](#in-game), [choosing settings for your PC](#hardware), and [validation](#validation).

[Back to contents](#contents)

<a id="hardware"></a>

## Choose settings for your PC

Use the limit you actually encounter, not a low-end/high-end label alone. The same GPU may be fast enough at 1080p and struggle with the same target at 1440p. A higher-priced PC can still stutter from heat, background work, or shader compilation.

### Find your specifications

- Press **Ctrl + Shift + Esc → Performance** in Task Manager. CPU shows the processor model; Memory shows installed RAM; GPU shows the graphics card and dedicated GPU memory. Shared GPU memory is not equivalent to dedicated VRAM.
- Open **Settings → System → Display → Advanced display**. Select your gaming monitor and confirm the resolution and refresh rate. Choose the intended supported refresh rate; a high-refresh screen can be left at 60 Hz accidentally.
- For NVIDIA, check **NVIDIA Control Panel → Set up G-SYNC**, if available, and your monitor's own Adaptive-Sync setting. A missing menu may depend on the display, connection, or GPU arrangement; do not assume all monitors support it.

### Pick a starting point

| Situation | First useful change | What to watch |
| --- | --- | --- |
| Entry-level GPU / limited VRAM | Low effects/shadows, modest texture budget; lower resolution if GPU limited | Texture pop-in, dedicated VRAM pressure, frame-time spikes |
| Balanced midrange system | Native resolution, low costly effects, sustainable cap, Reflex on NVIDIA | Busy-fight frame times and heat, not just range FPS |
| High-end GPU / high-refresh display | Start with the same baseline, then raise clarity settings with spare headroom | CPU limits, power/heat, and whether a higher cap stays stable |
| Laptop / integrated GPU | Use the proper power adapter and intended GPU; reduce resolution if needed | Thermal/power limits; integrated graphics share system RAM |
| High FPS but uneven motion | Compare a sustainable cap and, if available, the VRR profile | Cap overshoot, recurring spikes, tearing, shader warmup |

For texture budget, select a menu value below dedicated VRAM capacity with room for render targets and other assets. On an 8 GB card, a 4 GB budget is a reasonable initial comparison, not a requirement or a total-VRAM limit. Smaller cards should start lower. Raise it if memory headroom and measured results allow; selecting None is not automatically the smoothest option.

### Identify the bottleneck

A cap can make both CPU and GPU utilization low; that is normal. For a short controlled comparison, raise the cap above your observed FPS, keep other settings fixed, and compare two resolutions in the same scene. Restore the cap afterward.

- If lowering resolution noticeably improves FPS and the GPU was heavily loaded, rendering load is likely a limit. Reduce resolution or GPU-heavy settings first.
- If lowering resolution barely changes FPS, investigate CPU/game-thread load, other limits, temperatures, and background work. Overall CPU usage can look low while one critical thread is limiting performance.
- A utilization number alone is not a diagnosis. Record frame times and repeat the comparison after shader warmup.

Choose a cap your PC can usually sustain in demanding gameplay. There is no need to match monitor Hz exactly, and a cap cannot prevent every hitch. For VRR use the [presentation guide](#nvidia); for G-SYNC off, a below-refresh cap does not itself prevent tearing.

### Example PC specifications and settings

| Component / setting | Example value |
| --- | --- |
| CPU | AMD Ryzen 7 5700X3D |
| GPU | NVIDIA GeForce RTX 3060 Ti |
| System RAM | 32 GB |
| Monitor refresh | 360 Hz |
| Resolution | Not documented for this example; choose the display's native resolution initially |
| G-SYNC | Off |
| FPS cap | 170, set in Steam launch options |

For this example, use 170 FPS as the comparison baseline:

```text
+exec autoexec.cfg +fps_max 170
```

Keep `fps_max` commented in autoexec and NVIDIA Max Frame Rate off. A 170 FPS cap is valid on a 360 Hz monitor: it asks for a frame about every 5.88 ms, while the display refresh interval is about 2.78 ms. Those numbers are **not** total input latency, and fixed-refresh presentation can still tear or repeat frames unevenly. Do not switch to 357 FPS merely because the display is 360 Hz.

Start with in-game V-Sync off and Reflex Enabled. Compare Enabled + Boost while watching clocks and temperature. If 170 remains steady during demanding fights, compare a slightly higher target with identical captures; keep it only if pacing and responsiveness improve. If it repeatedly falls below 170, investigate the limiting component or try a lower cap. A more specific graphics target also depends on the chosen resolution.

#### NVIDIA screenshots provided as examples

Screenshots provided as examples show the Apex DX12 program profile, Fixed Refresh, highest available refresh, Low Latency Mode off, driver FPS cap off, V-Sync off, Prefer maximum performance, High performance texture filtering, sample/trilinear optimizations on, and Threaded optimization on. These are recorded settings, not measured improvements.

- Low Latency Mode off fits the proposed in-game Reflex workflow; the screenshot cannot confirm Reflex is enabled inside Apex.
- Keep your existing maximum-performance and texture-filtering choices as the baseline, then compare Normal power management and Quality filtering separately. Do not change several controls and attribute the result to one.
- Return Threaded optimization to Auto as a general default; forcing this OpenGL-oriented option on is not an established DX12 Apex improvement. OpenGL GDI compatibility is likewise not a useful Apex tuning target.
- Prefer application-controlled anisotropic filtering and antialiasing where supported, and choose their values in game. Controls marked unsupported for the application are not additional performance opportunities.
- The screenshot's “Highest available” setting does not prove Windows is currently using 360 Hz. Verify it in Advanced display.

Other readers should choose their own resolution, VRAM budget, cap, and presentation profile rather than copying this hardware example wholesale.

[Back to contents](#contents)

<a id="in-game"></a>

## In-game settings

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

The profile fragment requests `hud_setting_adsDof "0"` in an existing saved preference. Compare ADS screenshots using the same weapon, optic, distance, and scene after a restart. It is a best-effort blur preference, not proof of lower latency; some optics and post-processing may remain unchanged.

For hardware-specific starting points and how to check RAM versus VRAM, see [choosing settings for your PC](#hardware). For beginner file-editing and read-only behavior, see the [walkthrough](#beginners).

[Back to contents](#contents)

<a id="nvidia"></a>

## NVIDIA settings and frame pacing

Use NVIDIA Control Panel → Manage 3D settings → **Program Settings**, then select the executable your Apex installation actually runs. Browse to it if necessary; do not assume a fixed DX11/DX12 executable name. Record existing settings first. These profiles are starting points requiring on-PC validation.

### Choose a presentation profile

| Setting | Smooth, tear-free VRR | Latency-focused, tearing allowed |
| --- | --- | --- |
| Monitor support | G-SYNC / compatible VRR enabled in monitor and driver | VRR optional |
| Driver V-Sync | On | Off |
| In-game V-Sync | Off | Off |
| NVIDIA Reflex | Enabled; compare + Boost | Enabled; compare + Boost |
| FPS ceiling | Below refresh and within a sustainable frame rate | Highest sustainable rate with stable frame times; compare uncapped |

For VRR, begin around 3 FPS below refresh (141 at 144 Hz, 162 at 165 Hz, 237 at 240 Hz). These are examples, not universal optimums. Lower the ceiling if it overshoots the VRR range or fights cause persistent drops. Reflex with G-SYNC/V-Sync may already impose a lower ceiling; check observed FPS before adding another limiter. The goal is to stay inside the VRR range and avoid reaching the V-Sync ceiling.

For a display without VRR, the tear-free profile does not apply. Fixed-refresh V-Sync can prevent tearing but usually adds latency; choose deliberately. An FPS cap alone does not eliminate tearing.

Use `fps_max` in the autoexec **or** `+fps_max N` in launch options, not both. Leave driver Max Frame Rate and third-party limiters off when testing the game cap. If Reflex already limits below your chosen target, that lower observed rate can be expected. Avoid treating a refresh-minus-three cap as mandatory when V-Sync is off.

### Driver baseline

| Setting | Recommendation | Reason |
| --- | --- | --- |
| Image Scaling (NIS) | Off at native resolution initially | Optional spatial upscale when GPU limited; compare sharpness and frame times |
| DSR / DLDSR factors | Off for this baseline | Avoid rendering above native resolution for a performance-focused setup |
| Driver Ambient Occlusion | Off | Use the game's own control |
| Low Latency Mode | Off with in-game Reflex | Use the game's integrated latency control; do not assume stacking Ultra helps |
| Max Frame Rate | Off when using the game limiter | Keep cap ownership clear |
| Preferred refresh rate | Highest available, if shown | Also select the intended refresh in Windows |
| Power management | Normal initially | Test Prefer maximum performance per game if clocks fluctuate; watch heat |
| Texture filtering – Quality | Quality initially | Compare High performance only if its visual tradeoff earns measurable FPS |
| Anisotropic filtering / antialiasing | Application-controlled | Change graphics through the game |
| Driver FXAA / MFAA | Off initially | Avoid additional filtering overrides |
| Threaded optimization | Auto | Do not assume an OpenGL driver option improves Apex's DirectX renderer |
| Shader cache size | Driver default initially | Keep sufficient disk space; enlarge only for an identified cache issue |
| Triple buffering | Default / Off | The OpenGL option is not an Apex latency tweak |

Do not routinely delete shader caches. Warm up after a game or driver update before comparing stutter. Boost and maximum-performance power modes may increase power use; thermal throttling can erase their benefits. This repository does not apply global driver changes or import a driver profile automatically.

### How the referenced NVIDIA article is used

The GoodTechMaster article is dated 2022. Its application-controlled AA/filtering and Auto threaded-optimization recommendations fit this baseline. High performance texture filtering and larger shader caches remain optional comparisons, not guaranteed improvements. Its general Low Latency Mode discussion does not replace an Apex-specific Reflex setup, and frame caps can help pacing and VRR operation as well as power consumption. See [source decisions](#sources) for the differences.

Example driver settings and the 170 FPS / G-SYNC-off configuration are discussed in the [hardware guide](#hardware). Use that as a worked example, not a universal profile.

[Back to contents](#contents)

<a id="video-config"></a>

## Video configuration

Prefer the in-game menu: it generates settings appropriate to the current client. The root [videoconfig.txt](videoconfig.txt) is an optional **merge fragment**, not a complete replacement or an executable autoexec.

1. Apply [in-game settings](#in-game), exit Apex, and back up `%USERPROFILE%\Saved Games\Respawn\Apex\local\videoconfig.txt`. Use the actual Windows Saved Games location if it has been relocated.
2. Open the existing file. For each key in our fragment that already exists, edit its value inside the existing `VideoConfig` block. Do not add a second block or duplicate keys. If a key is absent, leave it out and use the corresponding menu control.
3. Preserve all other values, particularly resolution, display mode, refresh rate if present, `setting.stream_memory`, and `setting.configversion`.
4. Leave the file writable during initial setup and testing. Launch Apex, check the menu, play a short test, exit, and inspect what the client saved. A reverted value may indicate a renamed or unsupported setting; read-only cannot make an unsupported setting work.

| Key | Intended setting |
| --- | --- |
| `setting.mat_vsync_mode` | In-game V-Sync disabled; driver V-Sync depends on the selected profile |
| `setting.mat_antialias_mode` | Anti-aliasing disabled |
| `setting.volumetric_lighting` | Volumetric lighting disabled |
| `setting.particle_cpu_level` | Low effects detail |

These mappings come from the reference config and require a current-client check. The fragment deliberately omits upstream's fixed 2560×1440 resolution, texture allocation, config version, and undocumented shadow overrides. The ADS DoF preference is covered by the [profile fragment](profile.cfg), not the video fragment.

### Optional read-only after testing

See the [beginner walkthrough](#beginners) for right-click → Properties → Read-only instructions and how to remove the attribute. Read-only can protect saved values from ordinary writes, but pressing Apply in game can still change the live session and supersede overlapping autoexec settings. It does not lock every `.cfg` or automatically re-run autoexec. Fully restart and verify which values actually reload. Leave it writable when troubleshooting or allowing a client update to migrate the file.

[Back to contents](#contents)

<a id="steam"></a>

## Steam launch options

1. Library → Apex Legends → Manage → Browse local files. Open `cfg`.
2. Back up any existing autoexec and merge [autoexec.cfg](autoexec.cfg) into it, or copy ours if none exists.
3. Properties → General → Launch Options. Preserve a copy of your old arguments.

Start with:

```text
+exec autoexec.cfg
```

Optional 144 Hz VRR example, **only after selecting a sustainable cap**:

```text
+exec autoexec.cfg +fps_max 141
```

If using the launch-option cap, leave `fps_max` commented out in the autoexec. Replace 141 for your display and measured performance; see [NVIDIA settings](#nvidia).

Do not add `-high`, `-threads`, old renderer flags, or network overrides as a default. They are not established improvements for your PC. A launch argument being accepted does not prove every autoexec command executed; follow [validation](#validation).

### Optional intro skipping

The referenced Reddit comments suggest `-novid` after reporting that `-dev` stopped skipping the intro. You may test:

```text
-novid +exec autoexec.cfg
```

This is a community-reported startup convenience, not a verified FPS or latency improvement. Keep your chosen cap if you already use one. If the current client ignores `-novid`, remove it; it is not required to load the autoexec.

### Example Steam launch options: 170 FPS

For the example 5700X3D / RTX 3060 Ti / 360 Hz setup with G-SYNC off:

```text
+exec autoexec.cfg +fps_max 170
```

This demonstrates a 170 FPS Steam cap; choose a target appropriate to the PC and display. See the [hardware guide](#hardware) before changing it. For help finding folders or saving the file in Notepad, use the [beginner walkthrough](#beginners).

[Back to contents](#contents)

<a id="ea-app"></a>

## EA app launch options

Find Apex's installation folder through the EA app's game properties/manage menu, then open `cfg`. Back up and merge any existing autoexec before installing [autoexec.cfg](autoexec.cfg).

In the game's properties, locate Advanced launch options (the label can vary with app versions), save your previous arguments, and enter:

```text
+exec autoexec.cfg
```

The `+exec` command is passed to the game engine. The upstream guide lists `-exec` for EA; that distinction has not been verified for this guide, so this guide uses the usual engine command syntax and requires an execution check on your installation.

An optional cap uses `+fps_max N`, with N replaced by your selected integer target. For example, `+exec autoexec.cfg +fps_max 141` is a 144 Hz VRR starting example, not a universal preset. Leave `fps_max` commented in autoexec if you set it here. See [NVIDIA settings](#nvidia) and [validation](#validation).

### Optional intro skipping

The referenced Reddit comments suggest `-novid` after reporting that `-dev` stopped skipping the intro. You may test:

```text
-novid +exec autoexec.cfg
```

This is a community-reported startup convenience, not a verified FPS or latency improvement. Keep your chosen cap if you already use one. If the current client ignores `-novid`, remove it; it is not required to load the autoexec.

[Back to contents](#contents)

<a id="validation"></a>

## Validation and rollback

Repository checks only establish file structure and documentation consistency. They cannot establish command support, FPS improvements, input latency, or anti-cheat compatibility in a running game.

### Confirm the config loads

Fully exit and relaunch Apex after editing an autoexec. The referenced Reddit discussion reports that runtime `exec` keybinds stopped working; neither a reload bind nor an `echo` line is a reliable execution check.

Temporarily enable an obvious cap such as `fps_max "60"` in autoexec and remove other manual caps. Restart and check the firing range, where your baseline must previously have exceeded 60 FPS. A 60 FPS ceiling is evidence that the file executed, not that every command works. For a stronger check, repeat with a different cap such as 90 FPS if the uncapped baseline exceeds it; observed FPS should follow both changes after separate restarts. Restore your chosen cap after the check. If the check fails, verify the real installation folder, filename extension, launch arguments, and competing limits.

Check ADS DoF separately using identical before/after scenes and full restarts. Keep an unmodified backup. If no visible difference occurs, report the setting as unverified/ineffective on that client rather than adding unrelated rendering overrides.

For capture and sensor utility suggestions, see [optional tools](#tools). Use one capture tool consistently rather than stacking monitoring utilities.

### Compare performance

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

### Roll back

Close the game. Restore any edited autoexec, settings.cfg, profile.cfg, video config, and launch options from backup; if you had no autoexec before, remove the added file and its launch argument. Restore game and NVIDIA settings from your screenshots, or reset only the Apex driver profile if appropriate. Clear read-only on the video config if it was previously enabled. Restart and check the original behavior.

[Back to contents](#contents)

<a id="windows"></a>

## Windows and PC troubleshooting

Start here when measurements show a problem. These are diagnostic steps, not an extra list of mandatory FPS tweaks for low-end PCs.

### Useful checks before advanced tweaks

| Check | How / why |
| --- | --- |
| Correct refresh rate | Settings → System → Display → Advanced display; select the intended monitor and highest intended supported Hz |
| Drivers | Use NVIDIA/AMD and your motherboard/platform vendor's official sources. Record versions; investigate regressions before repeatedly changing drivers |
| Game files | Steam → Apex Properties → Installed Files → Verify integrity; EA app offers Repair under the game management menu |
| Background work | Check Task Manager for downloads, browser load, or unexpected CPU/disk activity; close unnecessary work before comparisons |
| Recording and overlays | Test optional recording/overlay features one at a time; keep measurement tools consistent |
| Storage and shaders | Keep free disk space, prefer an SSD for the game, and let shaders warm up after updates. Avoid routinely clearing shader caches |
| Temperature and clocks | Check for sustained thermal/power throttling during matches; improve airflow or fix cooling before software tweaks |
| Memory | Use the system-managed page file; 32 GB RAM is not a reason to disable it. If checking XMP/DOCP/EXPO, follow motherboard/RAM guidance and test stability; memory profiles are not universally stable |
| Mouse polling | Try 1000 Hz if very high polling coincides with CPU spikes; compare under the same conditions |
| Game Mode | Start with Windows Game Mode enabled. Treat HAGS changes as separate A/B tests requiring a restart, not a universal on/off fix |

Avoid blanket service-disabling scripts, registry “latency packs,” timer/HPET tweaks, process-priority forcing, or disabling security features for speculative gains. There is no need to add these to install a text config.

### Windows Fast Startup versus BIOS Fast Boot

| Feature | What it changes | When to investigate |
| --- | --- | --- |
| Windows Fast Startup | Shutdown can save kernel/driver state for reuse on the next boot | A problem appears after Shut down → power on but disappears after Restart |
| BIOS/UEFI Fast Boot | Firmware may skip or shorten hardware initialization checks | USB/device detection, firmware access, or boot initialization problems |

Neither setting is a reliable general FPS or latency improvement once a healthy system is running. Low-end or midrange hardware alone is not a reason to disable either. They are separate settings; changing one does not necessarily change the other.

#### Test Windows Fast Startup

First choose **Start → Power → Restart** and retest Apex. Restart performs a full Windows boot rather than using Fast Startup. If this consistently fixes a problem that returns after a shutdown/power-on cycle, test disabling Fast Startup:

1. Open **Control Panel → Hardware and Sound → Power Options**.
2. Select **Choose what the power buttons do**.
3. Select **Change settings that are currently unavailable**; Windows may require administrator approval.
4. Under Shutdown settings, untick **Turn on fast startup (recommended)** and choose **Save changes**.
5. Shut down, power on, and repeat the same test. Record whether it actually helps. Recheck the box to restore the previous behavior.

The option may be absent when hibernation is disabled or the system does not support it. Do not enable hibernation just to expose this checkbox. Disabling Fast Startup can lengthen boot time; it does not disable all BIOS fast-boot features.

#### Test BIOS/UEFI Fast Boot only for a relevant problem

Use your motherboard or PC manufacturer's manual to find **Fast Boot / Ultra Fast Boot**. Record its original value, disable only that option, save, and test. Restore the original value if it makes no useful difference. Names and entry keys vary; Windows Advanced startup may also offer **UEFI Firmware Settings**.

Do not change Secure Boot, TPM, storage mode, or unrelated firmware settings as part of this test. Firmware updates and other hardware changes are separate troubleshooting decisions, not prerequisites for using this repository.

Use the [validation guide](#validation) to separate a reproducible improvement from a single good match.

For O&O ShutUp10++, Winaero Tweaker, Autoruns, and measurement utilities, see [optional tools](#tools). These are optional diagnostic/customization choices, not prerequisites or guaranteed FPS improvements.

[Back to contents](#contents)

<a id="tools"></a>

## Optional tools

These tools are optional suggestions, not required steps or endorsed performance presets. These utilities have not been independently tested for this guide. Features and compatibility vary by release. Download from the official project/vendor links below, review current documentation, and avoid repackaged downloads or bundled “optimization packs.”

**Use at your own risk:** system-tweaking tools can affect Windows features, updates, devices, or startup software. Record your original settings, back up important files, and create a restore point if System Protection is available. A restore point is not a full backup and does not guarantee every change can be undone. Change one item at a time and keep a way to reverse it.

### Windows configuration and startup tools

| Tool | Useful for | Limits and precautions |
| --- | --- | --- |
| [O&O ShutUp10++](https://www.oo-software.com/en/shutup10) | Reviewing Windows privacy-related settings in one place | A privacy utility, not an established Apex FPS/latency fix. Read each setting's description and use its restore-point/export facilities where available. Avoid applying an entire preset blindly; some changes can affect services and Windows functionality |
| [Winaero Tweaker](https://winaerotweaker.com/) | Windows interface and behavior customization | Many options have no gaming benefit. Record each changed option and its original value; use the relevant reset control to undo it. Avoid speculative timer, security, update, or system-behavior changes simply because they are available |
| [Microsoft Sysinternals Autoruns](https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns) | Investigating what starts automatically, including entries beyond Task Manager's Startup apps | Start with inspection. Use signature verification and hide Microsoft entries to reduce clutter, but neither a third-party entry nor an unsigned file is automatically unnecessary or malicious. Uncheck an understood, nonessential entry rather than deleting it; recheck it to restore it. Leave unknown drivers, services, security software, and anti-cheat components alone |

For ordinary startup cleanup, try **Task Manager → Startup apps** first. Disable only apps you recognize and do not need at sign-in. A high startup-impact label describes startup work, not proof that an app is lowering FPS during a match. Do not use several tweaking utilities to change the same setting; that makes rollback harder to track.

### Measure before you tweak

| Tool | Useful for | Practical guidance |
| --- | --- | --- |
| [CapFrameX](https://www.capframex.com/) | Capturing and comparing FPS, frame-time plots, and low-percentile results | Use consistent capture duration, scene, and version. It measures frame delivery; an FPS result is not click-to-photon latency. Start with capture only, without extra overlay features |
| [Intel PresentMon](https://github.com/GameTechDev/PresentMon) | Frame presentation and supported performance telemetry across GPU vendors | An alternative to CapFrameX, not another recorder you need to run simultaneously. Available metrics depend on the system; label measured latency fields accurately |
| [HWiNFO](https://www.hwinfo.com/) | Checking temperatures, clock speeds, power limits, and memory readings | Sensors-only mode can help identify throttling. Avoid unnecessarily rapid polling; monitoring itself can add overhead. Keep the same monitoring setup for both comparison runs |
| [Microsoft Process Explorer](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer) | Investigating processes and unexpected background CPU activity | Inspect before acting. Do not terminate unfamiliar system or anti-cheat processes or force game priority as a blanket optimization |
| [LatencyMon](https://www.resplendence.com/latencymon) | Investigating driver/DPC/ISR behavior when audio dropouts or system-wide hitches occur | It evaluates real-time audio-related scheduling behavior, not mouse input latency or Apex responsiveness. A warning or named driver is a diagnostic lead, not proof of the cause; do not remove drivers solely on that result |

Start with Apex's performance display and Windows Task Manager. Add one capture tool and, only if needed, sensor logging. Do not install every tool in this table. Check current game and tool compatibility before using overlays; if a tool is blocked, do not attempt to bypass the restriction.

### A repeatable workflow

1. Capture a baseline using the [validation guide](#validation), including your current cap, resolution, temperatures, and background apps.
2. Identify a specific problem: recurring frame-time spikes, high temperatures, background CPU work, or unwanted Windows behavior.
3. Choose the relevant tool and inspect first. Write down one proposed change and how to undo it.
4. Make that one change. Restart if required and repeat the same capture after warming shaders.
5. Keep the change only if it produces a repeatable benefit or an intentional privacy/customization preference. Revert regressions and changes with no useful result.

Privacy preferences can be worthwhile without affecting FPS. Keep that reason separate from a performance claim. Avoid registry cleaners, automatic driver-updater bundles, RAM cleaners, and one-click service-disabling scripts as routine gaming maintenance.

For Windows Fast Startup, BIOS Fast Boot, and simpler checks, see [Windows troubleshooting](#windows).

[Back to contents](#contents)

<a id="screenshots"></a>

## Screenshot checklist

Screenshots should illustrate where to click and what a setting looks like. Label hardware-specific values **Example PC settings**; they are not universal targets. The following checklist describes captures to add to the guide, not images already embedded on this page.

### Most useful captures

| Capture | Where to open it | What should be visible |
| --- | --- | --- |
| Find the game installation | Steam → Library → right-click Apex → Manage → Browse local files | The menu item; a second image can show the opened `cfg` folder and `autoexec.cfg` |
| Set launch options | Steam → Apex → Properties → General | Launch Options field, showing the example `+exec autoexec.cfg +fps_max 170`; caption autoexec as optional and 170 as an example |
| Find saved settings | Windows + R → `%USERPROFILE%\Saved Games\Respawn\Apex\local` | The Run path, then File Explorer showing `settings.cfg` and `videoconfig.txt` with extensions visible |
| Find saved profile | Windows + R → `%USERPROFILE%\Saved Games\Respawn\Apex\profile` | File Explorer showing `profile.cfg`; make the different folder name clear |
| Edit a setting | Right-click the original `profile.cfg` → Open with → Notepad | The existing `hud_setting_adsDof` line and its value; show only relevant lines and edit only if the key exists |
| Save a new autoexec correctly | Notepad → File → Save As | Filename `autoexec.cfg`, Save as type **All files**, and the destination `cfg` folder; cancel if demonstrating over an existing file |
| Set optional read-only | Right-click `videoconfig.txt` → Properties → General | The file name, Read-only checkbox, and Apply button; caption that it protects the file, not live game settings |
| Verify display refresh | Windows Settings → System → Display → Advanced display | Selected gaming display, resolution, and refresh rate; caption values as an example |
| Configure graphics | Apex → Settings → Video / Advanced Video | Display mode, resolution, Reflex, V-Sync, adaptive resolution, texture budget, and the remaining graphics options; take overlapping images while scrolling |
| Configure the driver | NVIDIA Control Panel → Manage 3D settings → Program Settings → Apex | Apex selected and all relevant rows; use overlapping top/middle/bottom captures rather than tiny text in one image |

For the NVIDIA example, include Low Latency Mode, Max Frame Rate, Monitor Technology, Power management mode, Preferred refresh rate, texture filtering, and Vertical sync. Clearly label any example value that differs from the guide's starting recommendation, such as forced Threaded optimization On versus the recommended Auto.

### Optional extra captures

| Capture | Where / method | Purpose |
| --- | --- | --- |
| Show filename extensions | File Explorer → View → Show → File name extensions (Windows 11) | Explain how to spot `autoexec.cfg.txt` |
| EA app equivalent | Apex game management/properties → installation location and launch arguments | Cover readers using the other launcher; capture only an installed app's real UI |
| G-SYNC configuration | NVIDIA Control Panel → Set up G-SYNC, if available | Show whether enabled and which display is selected; do not change it just to match an example |
| Example hardware | Task Manager → Performance → CPU, Memory, GPU | Show model names and RAM/dedicated VRAM; multiple cropped images are clearer than one crowded screen |
| ADS blur comparison | Firing range, identical weapon/optic/position/aim point before and after the profile edit and full restart | Test whether the DoF preference has a visible effect; label game version and values, including if no change is observed |
| Frame-time comparison | The chosen capture tool's completed results page | Show the same capture duration and scene for baseline/candidate; include cap, resolution, average FPS, 1% low, and frame-time plot |
| Windows Fast Startup | Control Panel → Power Options → Choose what the power buttons do | Explain the optional troubleshooting checkbox, without implying it increases FPS |
| BIOS Fast Boot | The PC/motherboard's actual firmware page; use its screenshot feature or a clear photo | Optional and motherboard-specific; label model and firmware version, and avoid changing unrelated options |

### Capture and caption tips

Use **Windows + Shift + S** for a selected area, or the game's normal screenshot feature for a full-resolution ADS comparison. Save readable PNG images. Keep enough of the window title, folder path, or selected application to explain the context. Hide account names, email addresses, device serials, and personal folder names before sharing; leave setting names and values readable. Do not change a setting merely to take a screenshot.

Use short filenames such as `steam-launch-options.png`, `saved-games-local.png`, `videoconfig-read-only.png`, and `nvidia-program-settings-01.png`. When adding images to the repository, store them under `assets/screenshots/` and embed them next to the matching instructions in this README, with descriptive alt text.

Example caption: **Example PC settings — 5700X3D / RTX 3060 Ti, 170 FPS cap, G-SYNC off. Choose values suitable for the PC and display.** A screenshot shows a configuration; it does not demonstrate an FPS or latency gain by itself.

[Back to contents](#contents)

<a id="sources"></a>

## Sources and implementation notes

Reference review: 2026-10-07. Current-client behavior and performance remain unverified.

| Source | Use and access status |
| --- | --- |
| [240hz/ApexConfigs file layout](https://github.com/240hz/ApexConfigs/tree/4088cb3e11b4853d83b9947e81ac8a41479d15f3) | Historical file paths and example key locations inspected at commit `4088cb3e11b4853d83b9947e81ac8a41479d15f3` (2019-06-05). Used for layout reference only; its old exec-chain instructions and tuning claims are not adopted, and it does not verify current compatibility |
| [DominicKlmNL/apex-legends-config](https://github.com/DominicKlmNL/apex-legends-config) | Inspected README, configs, launcher guides, in-game guide, NVIDIA guide, and MIT license at commit `5d5ab6a0c93c3a9169b9f3c6f2d10e85b245f2b3` |
| [Reddit configuration discussion](https://www.reddit.com/r/apexlegends/comments/1w4ljsh/after_years_of_regularly_finetuning_my_pc_i/) | Reviewed a transcript of the post and comments; direct retrieval returned HTTP 403. Community reports are not controlled benchmarks. |
| [GoodTechMaster NVIDIA guide](https://www.goodtechmaster.com/ultimate-guide-nvidia-control-panel-optimization-for-gaming/) | Reviewed a copy of the article text, dated August 12, 2022; direct retrieval returned HTTP 403. General driver guidance, not current Apex-specific validation. |

The upstream author labels many commands as working. Those labels are upstream claims, not verification of this repository or the current client. This project matches the reference's main categories while curating its settings rather than mirroring every override.

### Deliberate differences

- Include `hud_setting_adsDof "0"`, already present upstream, in the profile merge fragment as an optional ADS blur preference. Do not invent a generic `dof 0` command.
- Keep `mat_depthfeather_enable "0"` commented as a separate legacy experiment. Depth feathering is not interchangeable with ADS depth of field.
- Leave the frame cap for hardware-specific selection instead of imposing upstream's 174 FPS target.
- Provide a merge-only video config, retaining the user's display, VRAM budget, and client schema.
- Offer separate VRR/tear-free and tearing-allowed presentation profiles. Avoid claiming one fixed cap maximizes every performance goal.
- Prefer menu controls and a minimal autoexec. Omit unverified network/prediction, telemetry, threading, ragdoll, decal, and forced texture overrides from the active config.
- Preserve personal mouse, audio, binds, FOV, and gameplay preferences; do not force upstream's 7.1 audio layout or autosprint.
- Avoid mandatory read-only configs, high process priority, global driver changes, or routine cache deletion.
- Use `+exec` for both launcher guides and explicitly flag the upstream EA `-exec` discrepancy for on-PC validation.

These are conservative implementation choices, not benchmark findings. See [validation](#validation) before claiming gains. Portions of the configuration are adapted from Downie2k's MIT-licensed work; the notice is retained in [third-party notice](#third-party). The existing project license is unchanged.

### Findings from the referenced articles

The Reddit discussion and NVIDIA article were reviewed from text copies after direct access returned HTTP 403. These copies do not establish that the live pages are unchanged or that their technical claims have been independently tested.

| Source observation | Decision for this repository |
| --- | --- |
| Reddit commenters flag a fixed 1440p video config | Keep the merge fragment and preserve the user's display settings |
| Reddit reports runtime `exec` binds no longer work; the author acknowledges removing the bind | Require a full game restart; do not add a reload bind or use `echo` as proof of execution |
| Reddit commenters report `-dev` no longer skips intros and suggest `-novid` | Document `-novid` as an optional, unverified startup convenience for both launchers |
| The Reddit author describes 174 FPS as a personal sweet spot | Keep hardware-specific cap selection; do not adopt the comment's refresh-minus-one examples as universal targets |
| A Reddit user initially blames audio tweaks for stutter, then retracts that diagnosis | Do not claim audio tweaks caused or cured it; use repeatable before/after measurements |
| The Reddit author links telemetry to wireless input problems | Treat this as an unmeasured anecdote; leave telemetry and texture eviction overrides out of the baseline |
| GoodTechMaster recommends application-controlled AA/filtering and Auto threaded optimization | Retain those baseline choices |
| GoodTechMaster recommends High performance texture filtering for shooters | Keep it as an A/B option because motion shimmer and image quality also matter |
| GoodTechMaster describes FPS caps mainly as a power-saving tool | Also account for GPU headroom, frame pacing, and staying within the VRR range |
| GoodTechMaster discusses driver Low Latency Mode without an Apex Reflex workflow | Prefer in-game Reflex; do not treat Ultra as an automatic FPS or smoothness improvement |
| GoodTechMaster suggests large shader caches | Keep the default unless cache pressure is identified; extra capacity does not guarantee fewer spikes |

The article also conflates NVIDIA Image Scaling with AI upscaling and describes a DirectX use for the driver's OpenGL triple-buffering control. Those explanations are not carried into this guide: NIS is spatial scaling/sharpening, and the Control Panel triple-buffering option is for OpenGL. DSR/DLDSR render above the chosen display resolution and can add substantial GPU work, so they are not part of the baseline. Driver availability and renderer support still determine whether a setting has any effect.

[Back to contents](#contents)

<a id="third-party"></a>

## Third-party notices

Configuration portions adapted from DominicKlmNL/apex-legends-config, commit 5d5ab6a0c93c3a9169b9f3c6f2d10e85b245f2b3.

Source: https://github.com/DominicKlmNL/apex-legends-config

MIT License

Copyright (c) 2026 Downie2k

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[Back to contents](#contents)

<a id="project-license"></a>

## Project license

The repository retains its existing [GPL-3.0 license](LICENSE). Upstream-derived settings are credited in [sources](#sources), with the upstream MIT notice preserved in [third-party notices](#third-party).
