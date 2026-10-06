> ⚠️ **Use at your own risk:** Back up your files and settings before changing anything. What works on one PC may make another run worse. Change one thing at a time, and undo it if it causes problems. FPS gains and command support are not guaranteed.

<h1 align="center">Apex Legends settings</h1>

<p align="center"><strong>More FPS. Less input delay. Smoother fights.</strong><br/>A step-by-step guide, from opening your first config file to checking what actually helps.</p>

<p align="center">
  <a href="#quick-setup"><strong>Start here</strong></a> &middot;
  <a href="#downloads"><strong>Downloads</strong></a> &middot;
  <a href="#beginners"><strong>File help</strong></a> &middot;
  <a href="#nvidia"><strong>FPS caps &amp; sync</strong></a> &middot;
  <a href="#notes"><strong>Notes</strong></a>
</p>

---

The aim is to keep Apex responsive and smooth when a fight gets busy. A high FPS number in the firing range is nice, but it doesn't help much if the game stutters as soon as a squad pushes.

If you've never opened a `.cfg` file, start with the [beginner walkthrough](#beginners). It shows where the files go, how to use Notepad, and how to undo a change. You don't need every tweak or tool on this page.

| Start with | Then | Check the result |
| --- | --- | --- |
| [Back up your files](#beginners) | [Set up the game](#in-game) and [choose an FPS cap](#nvidia) | [Compare before and after](#validation), including busy fights |

The example PC uses a **5700X3D · RTX 3060 Ti · 32 GB RAM · 360 Hz display**, with a **170 FPS cap and G-SYNC off**. These are example settings, not targets for every PC.

> [!NOTE]
> The config files haven't been tested in a running Apex client for this guide. Read the [autoexec support update](#autoexec-status) before using that optional file.

Inspired by [DominicKlmNL's Apex config](https://github.com/DominicKlmNL/apex-legends-config). Extra reading and explanations are in [Notes](#notes).

## Downloads

There are **four config files**, plus this README and the license.

> [!IMPORTANT]
> `settings.cfg`, `profile.cfg`, and `videoconfig.txt` contain only a few suggested lines. **Do not replace your complete game files with them.** Back up the original, find the matching line, and change its value. Replacing the whole file could wipe your binds, sensitivity, or other settings.

`autoexec.cfg` is optional. If you already have one, merge the lines you want rather than replacing your own file.

| File | Purpose | Exact destination | Raw file |
| --- | --- | --- | --- |
| [autoexec.cfg](autoexec.cfg) | Optional commands to try at startup; see the support note | `<Apex installation>\cfg\autoexec.cfg` | [Raw autoexec](https://raw.githubusercontent.com/WR3K/apex-legends-settings/main/autoexec.cfg) |
| [settings.cfg](settings.cfg) | Mouse-acceleration preference; keep your own binds and sensitivity | `%USERPROFILE%\Saved Games\Respawn\Apex\local\settings.cfg` | [Raw settings fragment](https://raw.githubusercontent.com/WR3K/apex-legends-settings/main/settings.cfg) |
| [videoconfig.txt](videoconfig.txt) | A few graphics settings; keep your own resolution and texture budget | `%USERPROFILE%\Saved Games\Respawn\Apex\local\videoconfig.txt` | [Raw video fragment](https://raw.githubusercontent.com/WR3K/apex-legends-settings/main/videoconfig.txt) |
| [profile.cfg](profile.cfg) | The ADS blur setting; keep your other preferences | `%USERPROFILE%\Saved Games\Respawn\Apex\profile\profile.cfg` | [Raw profile fragment](https://raw.githubusercontent.com/WR3K/apex-legends-settings/main/profile.cfg) |

`<Apex installation>` means the folder opened by Steam's **Browse local files** or the EA app's install-location control; it is not text to paste into Windows Run. The Saved Games paths can be pasted into Run and may differ if you relocated Saved Games. `profile.cfg` stores Apex preferences. It is **not** an NVIDIA profile to import into the driver.

For download and Notepad instructions, start with the [beginner walkthrough](#beginners).

## Contents

| Getting started | Game and graphics | Help and extra reading |
| --- | --- | --- |
| [Start here](#quick-setup) | [Choose settings for your PC](#hardware) | [Check whether a change helped](#validation) |
| [Downloads and file locations](#downloads) | [In-game settings](#in-game) | [Windows troubleshooting](#windows) |
| [Beginner walkthrough](#beginners) | [NVIDIA, G-SYNC, and FPS caps](#nvidia) | [Optional tools](#tools) |
| [Does autoexec still work?](#autoexec-status) | [Steam launch options](#steam) | [Advanced tuning](#advanced-tuning) |
| [Edit settings.cfg and profile.cfg](#saved-configs) | [EA app launch options](#ea-app) | [Screenshot checklist](#screenshots) |
| [Edit videoconfig.txt](#video-config) | [Notes](#notes) | [Credits](#third-party) · [License](#project-license) |

---

<a id="quick-setup"></a>

## Start here

If this is your first time changing config files, read the [file walkthrough](#beginners) first. Otherwise, here's the order to follow:

1. Run Apex once so it creates its settings files, then close it. Back up any files you plan to edit and take screenshots of your current game and NVIDIA settings.
2. Apply the [in-game starting settings](#in-game). Play a little and get a feel for how the game runs before adding anything else.
3. Choose the [G-SYNC/V-Sync setup](#nvidia) that matches how you want to play, then pick an FPS cap your PC can hold in busy fights.
4. If you want to try [autoexec.cfg](autoexec.cfg), put it in the game's `cfg` folder and add `+exec autoexec.cfg` to the launch options. It's optional; [check that it loads](#validation).
5. For the other three files, edit only the matching lines in your existing files. The [video guide](#video-config) and [settings/profile guide](#saved-configs) explain what goes where.
6. Fully restart Apex, check the settings, and compare against where you started. If a change makes things worse, undo it.

You don't need an installer or a pack of Windows tweaks to use these files.

[Back to contents](#contents)

<a id="autoexec-status"></a>

## Does autoexec still work?

**Update: 7 October 2026 — startup autoexec support is still unverified for this guide. It has not been confirmed removed.**

The linked Reddit discussion says that binds used to reload an `exec` file **while the game is running** stopped working. That is different from loading `autoexec.cfg` **when Apex starts**. The reference repository still describes startup loading, but that isn't a current in-game test.

The file stays available as an optional download. Its active settings are also in the game menus, so you can skip it and still use the rest of this guide. The ADS blur setting is in the `profile.cfg` snippet and doesn't need autoexec to run.

Before relying on it, use the [loading check](#validation). A file loading successfully doesn't mean every command in it still works—Apex updates can change that.

### If it doesn't load

1. Check the install folder, filename, and launch options first. `autoexec.cfg.txt` is the wrong filename.
2. If it still won't load, close Apex and remove `+exec autoexec.cfg` from Steam/EA launch options. Keep your FPS cap. For the 170 FPS example, that leaves `+fps_max 170`.
3. Move the added autoexec into your backup folder. If you merged it with an older file, restore that original instead.
4. Set **FOV Ability Scaling → Disabled** and **Sprint View Shake → Minimal** in the game menu, then restart.

Don't add reload binds or chain `exec` commands through the other settings files to try to force it. A blocked or removed command won't become supported just because it's in a different file. If reporting a problem, include the game version and what happened during the loading check.

[Back to contents](#contents)

<a id="saved-configs"></a>

## Editing settings.cfg and profile.cfg

These are files Apex saves for you. You don't need to add launch options to load them.

First, run the game, save your preferences, and close it normally. Press **Windows + R**, paste one of the folder paths below, and press Enter.

| Folder to open | File to edit | What to change |
| --- | --- | --- |
| `%USERPROFILE%\Saved Games\Respawn\Apex\local` | `settings.cfg` | If `m_acceleration` already exists, you can set it to `"0"` to request no mouse acceleration. Leave your binds, sensitivity, ADS multipliers, and other lines alone |
| `%USERPROFILE%\Saved Games\Respawn\Apex\profile` | `profile.cfg` | Find `hud_setting_adsDof` and, if it exists, set it to `"0"`. This requests no depth-of-field blur while aiming down sights |

Back up the file before editing. Use [Open with → Notepad](#beginners), change the existing value, and save. Don't add a second copy of the same line or replace your complete file with the short download.

For the ADS setting, restart Apex and compare the same weapon, optic, and scene. Some blur may remain, and the setting may be ignored on a particular game version. Judge it by what actually changes on screen.

### Can't find the file or setting?

Check that you've launched Apex using this Windows account. If Saved Games was moved, press **Windows + R** and enter `shell:SavedGames`, then look for `Respawn\Apex`.

If the game hasn't created a particular key, skip it. Don't create a full settings file from the snippet or assume pasting the line somewhere else will make it work. The file locations and example keys also appear in an [older community reference](#notes); the files your installed game creates are what you should work from.

Leave settings/profile writable while testing, and usually afterward too, so your binds and preferences can save. Making them read-only won't improve FPS. The mouse-acceleration line is a preference, not a proven latency fix. These snippets haven't been tested in a running client for this guide.

[Back to contents](#contents)

<a id="beginners"></a>

## Beginner walkthrough

A config file is just a text file with settings in it. You can open it in Notepad. The important part is putting it in the right folder and keeping a backup before editing anything.

### What the terms mean

| Term | Plain meaning |
| --- | --- |
| FPS | Frames the game produces each second; higher is useful when frames arrive consistently |
| Hz | How often your monitor refreshes each second; a 360 Hz screen does not make the PC render 360 FPS |
| Frame time | Time taken to produce a frame; sudden spikes feel like stutter |
| FPS cap | A limit on how many frames the game tries to produce, such as `+fps_max 170`; your PC can still drop below it |
| Latency | Delay between an action and its visible result; network ping is a separate contributor to online responsiveness |
| 1% low | A tool-dependent summary of the slowest frames; compare results using the same tool |
| VRAM / RAM | GPU memory for graphics / system memory; 32 GB RAM does not mean 32 GB VRAM |
| G-SYNC / FreeSync | Features that let a compatible monitor adjust refresh timing to frame delivery; collectively called variable refresh rate (VRR) |
| V-Sync | Controls frame presentation to prevent tearing; its latency tradeoff depends on the setup |
| Reflex | NVIDIA's supported in-game feature for reducing rendering-related latency |
| Autoexec / `.cfg` | A text file containing commands the game attempts to run at startup |
| Video config | The game's saved graphics settings, stored separately from its installed files |
| DoF / ADS | Depth of field (focus blur) / aiming down sights |

### Download this repository

On this repository's GitHub page, choose **Code → Download ZIP**. In File Explorer, right-click the downloaded ZIP → **Extract All**. Open the extracted folder. For one file, open it on GitHub and use **Download raw file**. If you save the normal webpage instead, you may download the webpage rather than the config.

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

Already have an autoexec? Keep a backup and add only the lines you want to change. Don't overwrite your binds or personal preferences. For video settings, follow the [merge guide](#video-config): the repository's `videoconfig.txt` is deliberately incomplete and must not replace your full file.

### Optional: set or remove read-only

Leave Read-only unticked while you work out which settings you want. Once you're happy with them and have a backup, you can tick it to help stop the game saving over that file. This is optional.

1. Close Apex and save the intended `videoconfig.txt` in Notepad.
2. In File Explorer, right-click **that file** → **Properties**.
3. On **General**, under **Attributes**, tick **Read-only**.
4. Click **Apply → OK**. To edit or save new permanent settings later, untick it and click **Apply → OK** first.

Use the file's checkbox, not the folder's checkbox. Do not mark the entire Apex folder read-only. An autoexec normally only needs to be read by the game; making it read-only is usually unnecessary.

#### What happens if you Apply graphics settings in game?

**Read-only protects the file on disk; it does not lock live settings in the running game.** Pressing Apply can change graphics for the current session even if those values cannot be written to the read-only video config. A menu change can also supersede an overlapping value previously set by autoexec. This does not mean the game edited the autoexec itself.

After a full restart, Apex normally reads its saved files again and tries to run any startup autoexec you set. That doesn't guarantee every value comes back exactly as expected: some commands may no longer work, another settings file may override them, or cloud sync may restore different values. Check what actually loads.

For a permanent change: close the game, remove read-only, edit the relevant file or apply settings in game, exit normally, inspect the saved values, and test another launch. Re-enable read-only only if you still want it. Remove read-only before troubleshooting resolution changes or letting a game update migrate the config schema.

Continue with [in-game settings](#in-game), [choosing settings for your PC](#hardware), and [validation](#validation).

[Back to contents](#contents)

<a id="hardware"></a>

## Choose settings for your PC

Start with what your PC is struggling with. The same graphics card might hold your target FPS at 1080p but struggle at 1440p. An expensive PC can still stutter because of heat, background apps, or the game preparing graphics data after an update.

### Find your specifications

- Press **Ctrl + Shift + Esc → Performance** in Task Manager. CPU shows the processor model; Memory shows installed RAM; GPU shows the graphics card and dedicated GPU memory. Shared GPU memory is not equivalent to dedicated VRAM.
- Open **Settings → System → Display → Advanced display**. Select your gaming monitor and confirm the resolution and refresh rate. Choose the intended supported refresh rate; a high-refresh screen can be left at 60 Hz accidentally.
- For NVIDIA, check **NVIDIA Control Panel → Set up G-SYNC**, if available, and your monitor's own Adaptive-Sync setting. A missing menu may depend on the display, connection, or GPU arrangement; do not assume all monitors support it.

### Pick a starting point

| Situation | First useful change | What to watch |
| --- | --- | --- |
| Entry-level GPU / limited VRAM | Low effects/shadows, modest texture budget; lower resolution if GPU limited | Texture pop-in, dedicated VRAM pressure, frame-time spikes |
| Balanced midrange system | Native resolution, low shadows/effects, a cap the PC can hold, Reflex on NVIDIA | Busy-fight frame times and heat, not just range FPS |
| High-end GPU / high-refresh display | Start with the same settings, then raise clarity settings with spare headroom | CPU limits, power/heat, and whether a higher cap stays stable |
| Laptop / integrated GPU | Use the proper power adapter and intended GPU; reduce resolution if needed | Thermal/power limits; integrated graphics share system RAM |
| High FPS but uneven motion | Try a cap the PC can hold and, if supported, the G-SYNC/FreeSync tear-free setup | Cap overshoot, recurring spikes, tearing, shader warmup |

For texture budget, select a menu value below dedicated VRAM capacity with room for render targets and other assets. On an 8 GB card, a 4 GB budget is a reasonable initial comparison, not a requirement or a total-VRAM limit. Smaller cards should start lower. Raise it if memory headroom and measured results allow; selecting None is not automatically the smoothest option.

### Is the CPU or graphics card holding FPS back?

If your PC is hitting its FPS cap, low CPU or GPU usage can be normal—it doesn't need to work harder. To investigate a limit, briefly raise the cap above the FPS you're getting and compare two resolutions in the same scene. Change nothing else, then restore the cap afterward.

- If lowering resolution gives a clear FPS increase and the graphics card was working hard, try reducing resolution, shadows, or other graphics settings.
- If lowering resolution barely helps, check CPU load, temperatures, background apps, and other limits. Overall CPU usage can look low even when one part of the game's work is holding everything else up.
- Don't decide from one usage number. Let the game warm up and repeat the comparison, including how smoothly the frames arrive.

Choose a cap your PC can usually hold in busy fights. There is no need to match monitor Hz exactly, and a cap cannot prevent every hitch. If G-SYNC or FreeSync is enabled, use the [sync and FPS-cap guide](#nvidia). With those features disabled and V-Sync off, a below-refresh cap does not itself prevent tearing.

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

Open Apex's video settings and use this as a starting point. Menu names can change after updates. Start at your monitor's native resolution—the resolution it was designed to display—and lower it if the graphics card can't keep up.

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

Keep the sensitivity, aim settings, keybinds, audio setup, and gameplay preferences you're comfortable with. Start with 1000 Hz mouse polling if supported; higher rates can increase CPU load. Mouse polling does not prescribe a texture streaming budget. Use the game's performance display to monitor FPS and network behavior, but do not equate ping with input latency.

The [profile snippet](#saved-configs) changes an existing `hud_setting_adsDof` value to `"0"` to try to reduce blur while aiming. Compare ADS screenshots using the same weapon, optic, distance, and scene after a restart. It may not remove every blur effect, and a sharper picture doesn't prove input delay is lower.

For hardware-specific starting points and how to check RAM versus VRAM, see [choosing settings for your PC](#hardware). For beginner file-editing and read-only behavior, see the [walkthrough](#beginners).

[Back to contents](#contents)

<a id="nvidia"></a>

## NVIDIA settings, G-SYNC, and FPS caps

Open **NVIDIA Control Panel → Manage 3D settings → Program Settings** and select Apex. This lets you change settings for Apex without changing every other game. If it isn't listed, use **Add / Browse** and select the game's actual executable from its install folder; the filename can change between game versions. Take a screenshot of the current settings first.

### Which sync setup are you using?

**G-SYNC/FreeSync and V-Sync aren't the same switch.** G-SYNC or FreeSync lets a supported monitor adjust when it refreshes to match arriving frames. That's what **variable refresh rate (VRR)** means. V-Sync controls when frames are shown to prevent tearing—the visible split where parts of different frames appear on screen together. You can turn V-Sync off and still have G-SYNC enabled.

On NVIDIA, check **Control Panel → Set up G-SYNC**, the monitor's Adaptive-Sync setting, and **Manage 3D settings → Program Settings → Apex → Vertical sync**. Check Apex's in-game V-Sync separately. On AMD, look for **AMD FreeSync** in the display settings of AMD Software and the monitor menu; NVIDIA-specific Reflex and driver controls do not apply.

Notice that **in-game V-Sync is off in both examples below**. Check G-SYNC and the NVIDIA driver's V-Sync setting too; “V-Sync off in Apex” doesn't tell you the whole setup.

| Setting | G-SYNC enabled: prioritize tear-free play | G-SYNC disabled: prioritize responsiveness, allow tearing |
| --- | --- | --- |
| Monitor / driver | Enable supported G-SYNC or G-SYNC Compatible operation | G-SYNC off / Fixed Refresh |
| Driver V-Sync | On | Off |
| In-game V-Sync | Off | Off |
| NVIDIA Reflex | Enabled; compare + Boost | Enabled; compare + Boost |
| FPS cap | Below the monitor's maximum refresh rate, at a value the PC can hold | Start with a value the PC can hold; compare a higher cap or no cap |

#### If G-SYNC is enabled and driver V-Sync is on

Begin with a cap slightly below maximum refresh, such as 141 FPS at 144 Hz, 162 at 165 Hz, or 237 at 240 Hz. These are starting examples, not required values. Reflex with G-SYNC and V-Sync may already impose a lower ceiling; check observed FPS before adding another limiter. Lower the cap further if it overshoots the display's supported range or fights cause persistent drops. The aim is to stay below the monitor's maximum refresh rate, where V-Sync can start making frames wait.

If you use AMD FreeSync, the aim is also to stay within the refresh rates your monitor supports. Use the controls in AMD Software and test the result; NVIDIA-only options such as Reflex won't apply.

#### If G-SYNC/FreeSync is disabled and V-Sync is off

Use a cap that gives repeatable, stable frame times on that PC. There is no automatic “refresh minus three” rule for this setup. The example 360 Hz screen with a 170 FPS cap belongs here. Try another cap the PC can hold if useful, but neither 170 nor an exact fraction such as 180 guarantees tear-free output: an FPS limiter alone does not synchronize frame delivery to the display.

If **G-SYNC/FreeSync is enabled but V-Sync is off**, the monitor can still adjust its refresh rate within its supported range. You may still see tearing, especially near the limits of that range. That's different from turning G-SYNC/FreeSync off completely. If both features are disabled and tearing is unacceptable, consider supported G-SYNC/FreeSync or ordinary V-Sync with its latency tradeoff.

Use `fps_max` in the autoexec **or** `+fps_max N` in launch options, not both. Leave driver Max Frame Rate and third-party limiters off when testing the game cap. If Reflex already limits below the chosen target, that lower observed rate can be expected.

### Other NVIDIA settings to start with

| Setting | Recommendation | Reason |
| --- | --- | --- |
| Image Scaling (NIS) | Off at native resolution initially | Can enlarge a lower-resolution image to fit the screen; test the look and performance if the GPU is struggling |
| DSR / DLDSR factors | Off to start with | Avoid rendering above native resolution for a performance-focused setup |
| Driver Ambient Occlusion | Off | Use the game's own control |
| Low Latency Mode | Off with in-game Reflex | Use the game's integrated latency control; do not assume stacking Ultra helps |
| Max Frame Rate | Off when using the game limiter | Set the cap in one place so you know which setting controls it |
| Preferred refresh rate | Highest available, if shown | Also select the intended refresh in Windows |
| Power management | Normal initially | Test Prefer maximum performance per game if clocks fluctuate; watch heat |
| Texture filtering – Quality | Quality initially | Try High performance if you want; keep it only if extra FPS is worth the change in how textures look |
| Anisotropic filtering / antialiasing | Application-controlled | Change graphics through the game |
| Driver FXAA / MFAA | Off initially | Avoid additional filtering overrides |
| Threaded optimization | Auto | Do not assume an OpenGL driver option improves Apex's DirectX renderer |
| Shader cache size | Driver default initially | Keep sufficient disk space; enlarge only for an identified cache issue |
| Triple buffering | Default / Off | The OpenGL option is not an Apex latency tweak |

Do not routinely delete shader caches. Warm up after a game or driver update before comparing stutter. Boost and maximum-performance power modes may increase power use; thermal throttling can erase their benefits. This repository does not apply global driver changes or import a driver profile automatically.

### How the referenced NVIDIA article is used

The GoodTechMaster article is dated 2022. Its application-controlled AA/filtering and Auto threaded-optimization recommendations fit this baseline. High performance texture filtering and larger shader caches remain optional comparisons, not guaranteed improvements. Its general Low Latency Mode discussion does not replace an Apex-specific Reflex setup, and frame caps can help frames arrive more evenly, keep G-SYNC/FreeSync within the display's supported range, and reduce power use. See [notes](#notes) for the differences.

Example driver settings and the 170 FPS / G-SYNC-off configuration are discussed in the [hardware guide](#hardware). Use that as a worked example, not a universal profile.

[Back to contents](#contents)

<a id="video-config"></a>

## Editing videoconfig.txt

Start with the in-game graphics menu. It writes the settings in the format your current Apex version expects. Editing `videoconfig.txt` is optional.

The [download](videoconfig.txt) contains only four suggested settings. **Don't replace your complete video config with it.**

1. Apply the [in-game settings](#in-game), then close Apex.
2. Press **Windows + R**, paste `%USERPROFILE%\Saved Games\Respawn\Apex\local`, and open it. Back up `videoconfig.txt`.
3. Open your original in Notepad. Find the matching keys from the table below and change their values. If a key isn't there, skip it and use the game menu.
4. Keep the existing `VideoConfig` block and braces. Don't add a second block or duplicate keys.
5. Leave your resolution, display mode, texture memory budget (`setting.stream_memory`), version (`setting.configversion`), and all other values as they are.
6. Save, restart Apex, and check the menu and a short match. Exit normally and look at what the game saved afterward.

| Key | Value in the snippet | Intended change |
| --- | --- | --- |
| `setting.mat_vsync_mode` | `0` | In-game V-Sync off; driver V-Sync depends on the [setup you choose](#nvidia) |
| `setting.mat_antialias_mode` | `0` | Anti-aliasing off |
| `setting.volumetric_lighting` | `0` | Volumetric lighting off |
| `setting.particle_cpu_level` | `0` | Low effects detail |

These mappings come from the reference config and still need checking in the current game. If a value keeps changing back, it may have changed meaning or stopped being supported. Read-only won't fix that.

Once you're happy with the settings, you can use the [optional read-only steps](#beginners). Leave the file writable while testing and when a game update needs to update its format. The ADS blur line belongs in the [profile snippet](#saved-configs), not this file.

[Back to contents](#contents)

<a id="steam"></a>

## Steam launch options

In Steam, right-click **Apex Legends → Properties → General**. Find **Launch Options** and save a copy of anything already in the box.

If you're using the optional autoexec, first put it in **Manage → Browse local files → cfg**, then add:

```text
+exec autoexec.cfg
```

### Adding an FPS cap

`+fps_max` tells the game the highest FPS you want it to render. It doesn't guarantee your PC can hold that number.

For the example 170 FPS setup:

```text
+exec autoexec.cfg +fps_max 170
```

If you're skipping autoexec, just use:

```text
+fps_max 170
```

Replace 170 with the target you chose in the [FPS-cap guide](#nvidia). For example, 141 FPS is one starting point for a 144 Hz screen with G-SYNC enabled and driver V-Sync on. It isn't the right cap for every PC.

If the cap is set here, leave `fps_max` commented out in autoexec and the driver's Max Frame Rate setting off. Keeping it in one place makes troubleshooting much easier.

### Skipping the intro

The Reddit comments suggest `-novid` after reporting that `-dev` stopped skipping the intro. You can try:

```text
-novid +exec autoexec.cfg +fps_max 170
```

Keep only the parts you're using. Intro skipping is a startup convenience, not an FPS tweak. If the game ignores `-novid`, remove it.

Leave `-high`, `-threads`, old renderer flags, and network overrides out of the starting setup. There's no demonstrated benefit for your PC just because another guide lists them.

[Back to contents](#contents)

<a id="ea-app"></a>

## EA app launch options

Open Apex's game properties/manage menu in the EA app. Find the installation location and open its `cfg` folder if you're using autoexec. Back up an existing autoexec before merging any lines.

In the game properties, find **Advanced launch options** or the similarly named field. Save a copy of the old arguments, then use the same starting command:

```text
+exec autoexec.cfg
```

To include an example 170 FPS cap:

```text
+exec autoexec.cfg +fps_max 170
```

Choose your own cap using the [FPS-cap guide](#nvidia). If you don't use autoexec, remove `+exec autoexec.cfg` and keep only the cap. If the cap is set in launch options, leave it commented out in autoexec.

The upstream guide lists `-exec` for EA. That launcher-specific difference hasn't been verified, so this guide uses the usual engine command `+exec` and asks you to [check that it loads](#validation).

You can also try `-novid` for intro skipping, as reported in the Reddit comments. It's optional, isn't verified here, and doesn't improve in-match FPS. EA app menu names can change between versions.

[Back to contents](#contents)

<a id="validation"></a>

## Check whether a change actually helped

Try to change one thing at a time. If you change ten settings and the game feels worse, it's hard to know which one to undo.

### Check that autoexec loads

Fully exit and restart Apex after editing it. The referenced Reddit discussion reports that mid-game reload binds stopped working, and an `echo` line isn't a useful loading check without a visible console or log.

If your PC normally runs above 60 FPS in the firing range, temporarily set `fps_max "60"` in autoexec. Remove other manual FPS caps for this test, restart, and see whether the game now stops around 60 FPS. Repeat with 90 if your PC normally exceeds it. If the observed ceiling follows both changes after separate restarts, that's evidence the file loaded.

Restore your chosen cap afterward. This checks the file loading, not every command inside it. If it fails, use the [autoexec troubleshooting steps](#autoexec-status).

### Check the ADS blur setting separately

Use the same weapon, optic, position, and aim point before and after the profile edit, with a full restart between them. If there's no visible difference, record that result. Don't assume a line worked just because it stayed in the file.

### Compare performance

1. Write down your game/driver versions, hardware, resolution, refresh rate, FPS cap, Reflex setting, and whether G-SYNC/FreeSync and both V-Sync controls are on or off.
2. Let the game warm up, especially after an update. Run the same firing-range route for three captures of 60–120 seconds per setup. Keep background apps and recording tools the same.
3. Compare average FPS, 1% lows, and frame-time spikes using the same [capture tool](#tools). Watch temperatures and GPU memory use too.
4. Play some real matches. A setting that looks great in an empty firing range may still struggle during a busy fight.
5. Keep changes that help repeatedly. Undo changes that make things worse or add problems without a useful improvement.

**Frame time** is how long a frame takes to arrive. Sudden spikes are often what you feel as a hitch, even when the average FPS looks high. **1% lows** describe the slow end of performance; tools calculate them differently, so compare results from the same tool.

The in-game FPS display is a useful starting point, but it won't give you every measurement above. FPS and ping also aren't measurements of the full delay from clicking your mouse to seeing the result. Use supported latency telemetry or suitable measurement equipment for that, and say exactly what was measured.

| Date / game version | Settings / cap | Average FPS | 1% low | Spikes or tearing | Latency method + result | Temperatures |
| --- | --- | --- | --- | --- | --- | --- |
| Not tested yet | Original settings | — | — | — | Not measured | — |
| Not tested yet | Changed settings | — | — | — | Not measured | — |

### Something feels worse? Go back

Close Apex. Restore the original files and launch options from your backup, along with the in-game and NVIDIA settings you recorded. If you didn't have an autoexec before, remove the added file and its launch argument. If you did, restore the original.

Remove read-only from any file that needs editing, restart, and check that the old behavior is back. Don't keep a tweak just because it sounds more “competitive.”

[Back to contents](#contents)

<a id="windows"></a>

## Windows and PC troubleshooting

If the game still hitches, check these before adding more config commands. You don't need to change everything here just because the PC is older.

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

Turning these off isn't a general FPS boost, even on a lower-end PC. They're worth checking when the problem depends on how the PC started up. They are separate settings, so changing one doesn't necessarily change the other.

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

You don't need to download everything in this list. Pick a tool only when you have a reason to use it. Some help measure performance; others change Windows preferences and may do nothing for FPS. They haven't been independently tested for this guide. Use the official links below and check that the current version supports your system.

Windows-tweaking tools can affect updates, devices, startup apps, and other features. Record your original settings, back up important files, and create a restore point if System Protection is available. A restore point is not a full backup and does not guarantee every change can be undone. Change one item at a time and keep a way to reverse it.

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

Changing a privacy setting is fine if that's what you want. Just don't assume it will make Apex faster. Avoid registry cleaners, automatic driver-updater bundles, RAM cleaners, and one-click service-disabling scripts as routine gaming maintenance.

For Windows Fast Startup, BIOS Fast Boot, and simpler checks, see [Windows troubleshooting](#windows).

[Back to contents](#contents)

<a id="advanced-tuning"></a>

## Want to go further? Optional advanced tuning

If the game is already running well, you can stop there. The guides below go much further into PC tuning. Read them as background, not as a list of things every Apex player needs to do. You don't need to overclock, flash a BIOS, or edit the Windows registry to use these config files.

- [Calypto's Latency Guide](https://docs.google.com/document/d/1c2-lUJq74wuYK1WrA_bIvgb89dUN0sj8-hO3vqmrau4/edit?usp=sharing) covers background processes, driver scheduling, input, displays, and extensive system changes. The PDF copy contains advice for several Windows and hardware generations; check applicability before using any recommendation.
- [A slightly better way to overclock and tweak your Nvidia GPU](https://docs.google.com/document/d/14ma-_Os3rNzio85yBemD-YSpF_1z75mZJz1UdzmW8GE/edit?usp=sharing), by Cancerogeno, includes a **mid-2026 update** on newer RTX cards followed by its older Pascal/Turing guide. The example RTX 3060 Ti is **Ampere**, so neither an old Pascal/Turing voltage example nor an RTX 40/50-series result is a ready-made preset for it.

Both PDF copies were reviewed for this guide. Direct access to the Google Docs links returned HTTP 403, so their live revisions were not checked. The [notes](#notes) explain which points informed the recommendations.

### What to take from these guides

Measure the actual game, manage unnecessary background work, monitor cooling and sustained performance, and compare one change at a time. Higher reported clocks, a flatter voltage graph, or a lower LatencyMon number alone do not establish lower input latency or smoother Apex gameplay.

LatencyMon is useful for investigating driver scheduling and audio dropouts; it does **not** measure the full delay from a mouse click to the screen changing. A mouse polling graph also does not measure game frame pacing. Use the matching measurement for the question being tested, and keep repeated results rather than restarting tests until a preferred minimum appears.

### Optional GPU tuning: compare against stock

A GPU overclock runs part of the GPU faster than its stock setting. An undervolt attempts a chosen operating point at lower voltage and may reduce power or heat, but either can cause crashes, visual errors, or worse performance. Stock settings are the default recommendation for a general-purpose guide.

For experienced readers choosing to experiment:

1. Record a stock baseline after shader warmup, including frame times, GPU temperature, fan noise, and clocks. Save the original software profile. Do not enable automatic application of experimental settings at Windows startup.
2. Inspect cooling and any reported temperature/power limits first. A power-limit indicator can be normal boost behavior; it is not itself a fault to remove.
3. Make one small, reversible software change within the card manufacturer's limits. No fixed voltage, core offset, memory offset, or maximum-slider preset is recommended for every GPU. Keep temperature and electrical protections enabled.
4. Retest a repeatable graphics workload, actual Apex matches, and light/heavy scene transitions. A short successful stress test does not prove long-term stability. Check completed work and frame times, not just clock readings; memory tuning can lose performance before obvious artifacts appear.
5. Revert on artifacts, driver resets, crashes, errors, excessive heat/noise, or worse results. Return to the recorded stock profile and retest. Keep the stable stock option available even if a tuned profile appears better.

### Tools for this optional work

| Tool | Use | Limit |
| --- | --- | --- |
| [MSI Afterburner](https://www.msi.com/Landing/afterburner/graphics-cards) | GPU monitoring and supported software clock/fan adjustments | Settings and controls vary by GPU; avoid applying another card's profile or auto-applying untested settings |
| [GPU-Z](https://www.techpowerup.com/gpuz/) | Identify the GPU and inspect supported sensors and performance-limit indicators | Useful for inspection; a sensor reading does not justify flashing firmware |
| [OCCT](https://www.ocbase.com/) | Controlled stress/error testing | Check temperature and power during testing; passing one test cannot establish stability in every workload |

### What to leave out of a basic setup

The linked guides include blanket SMT/CPU-idle changes, timer and interrupt-affinity edits, security-feature disabling, GPU BIOS changes, and attempts to suppress thermal downclocking. These can reduce performance, break devices or Windows, weaken protection, or damage hardware. They are not part of the repository's baseline. In particular, do not disable GPU overheat protection or flash another card's BIOS to follow this guide.

Keep SMT enabled by default on the example 5700X3D; investigate a specific scheduling problem with controlled measurements rather than treating SMT-off as a universal improvement. Keep Reflex Enabled as the starting point and compare + Boost on the actual PC; neither mode is automatically best for every workload.

[Back to contents](#contents)

<a id="screenshots"></a>

## Screenshot checklist

Screenshots are most useful when they show exactly where to click and what to look for. Label hardware-specific values **Example PC settings**; they are not universal targets. The following checklist describes captures to add to the guide, not images already embedded on this page.

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

<a id="notes"></a>

## Notes

Reference review: 2026-10-07. Current-client behavior and performance remain unverified.

| Reference | What to know |
| --- | --- |
| [Calypto's Latency Guide](https://docs.google.com/document/d/1c2-lUJq74wuYK1WrA_bIvgb89dUN0sj8-hO3vqmrau4/edit?usp=sharing) | Reviewed the PDF copy. Background for latency diagnostics and display behavior; broad system-tweak and hardware claims are not independently verified. Direct Google Docs access returned HTTP 403 |
| [A slightly better way to overclock and tweak your Nvidia GPU](https://docs.google.com/document/d/14ma-_Os3rNzio85yBemD-YSpF_1z75mZJz1UdzmW8GE/edit?usp=sharing) | Reviewed the PDF copy by Cancerogeno, including its mid-2026 update and older Pascal/Turing sections. No proposed tuning was executed or benchmarked. Direct Google Docs access returned HTTP 403 |
| [240hz/ApexConfigs file layout](https://github.com/240hz/ApexConfigs/tree/4088cb3e11b4853d83b9947e81ac8a41479d15f3) | Historical file paths and example key locations inspected at commit `4088cb3e11b4853d83b9947e81ac8a41479d15f3` (2019-06-05). Used for layout reference only; its old exec-chain instructions and tuning claims are not adopted, and it does not verify current compatibility |
| [DominicKlmNL/apex-legends-config](https://github.com/DominicKlmNL/apex-legends-config) | Inspected README, configs, launcher guides, in-game guide, NVIDIA guide, and MIT license at commit `5d5ab6a0c93c3a9169b9f3c6f2d10e85b245f2b3` |
| [Reddit configuration discussion](https://www.reddit.com/r/apexlegends/comments/1w4ljsh/after_years_of_regularly_finetuning_my_pc_i/) | Reviewed a transcript of the post and comments; direct retrieval returned HTTP 403. Community reports are not controlled benchmarks. |
| [GoodTechMaster NVIDIA guide](https://www.goodtechmaster.com/ultimate-guide-nvidia-control-panel-optimization-for-gaming/) | Reviewed a copy of the article text, dated August 12, 2022; direct retrieval returned HTTP 403. General driver guidance, not current Apex-specific validation. |

The upstream author labels many commands as working. Those labels are upstream claims, not verification of this repository or the current client. This project matches the reference's main categories while curating its settings rather than mirroring every override.

<details>
<summary><strong>Why some recommendations differ from the linked guides</strong></summary>


- Include `hud_setting_adsDof "0"`, already present upstream, in the profile merge fragment as an optional ADS blur preference. Do not invent a generic `dof 0` command.
- Keep `mat_depthfeather_enable "0"` commented as a separate legacy experiment. Depth feathering is not interchangeable with ADS depth of field.
- Leave the frame cap for hardware-specific selection instead of imposing upstream's 174 FPS target.
- Provide a merge-only video config, retaining the user's display, VRAM budget, and client schema.
- Offer separate G-SYNC-enabled/tear-free and G-SYNC-disabled/tearing-allowed presentation profiles. Avoid claiming one fixed cap maximizes every performance goal.
- Prefer menu controls and a minimal autoexec. Omit unverified network/prediction, telemetry, threading, ragdoll, decal, and forced texture overrides from the active config.
- Preserve personal mouse, audio, binds, FOV, and gameplay preferences; do not force upstream's 7.1 audio layout or autosprint.
- Avoid mandatory read-only configs, high process priority, global driver changes, or routine cache deletion.
- Use `+exec` for both launcher guides and explicitly flag the upstream EA `-exec` discrepancy for on-PC validation.

These choices keep the setup easier to understand and undo; they aren't benchmark results. See [validation](#validation) before claiming gains. Portions of the configuration are adapted from Downie2k's MIT-licensed work; the notice is retained in [third-party notice](#third-party). The existing project license is unchanged.

### Comparing the advice

The Reddit discussion and NVIDIA article were reviewed from text copies after direct access returned HTTP 403. These copies do not establish that the live pages are unchanged or that their technical claims have been independently tested.

| Advice in the guide | How it is used here |
| --- | --- |
| Calypto emphasizes background work, cooling, and measuring changes | Retain controlled before/after checks, while distinguishing driver scheduling from game/input latency |
| Calypto uses LatencyMon averages and mouse polling plots as latency/smoothness targets | Use them for their diagnostic scope; do not equate them with click-to-photon latency or Apex frame times |
| Calypto suggests caps at refresh-rate factors with adaptive sync off, or about 10% below maximum refresh with it on | Treat cap values as experiments. An unsynchronized limiter does not lock the display timing; neither an exact fraction nor a fixed percentage guarantees smoothness. Keep the measured, sustainable-cap approach |
| Calypto recommends broad SMT, power-state, security, timer, and driver changes | Do not adopt these as default Windows/Apex setup; diagnose a specific problem first |
| The GPU guide's mid-2026 update revises its older Pascal/Turing approach | Label generation-specific advice; do not present old voltage points or newer-card offsets as RTX 3060 Ti presets |
| The GPU guide discusses cooling, stock/tuned comparisons, clocks, and stress tests | Add an optional comparison workflow, with stock settings as the baseline and performance/stability as the outcome |
| The GPU guide includes maximum sliders, VBIOS flashing, clock-policy changes, and disabling overheat slowdown | Do not adopt these as generic instructions; retain manufacturer limits and thermal protections |
| Reddit commenters flag a fixed 1440p video config | Keep the merge fragment and preserve the user's display settings |
| Reddit reports runtime `exec` binds no longer work; the author acknowledges removing the bind | Require a full game restart; do not add a reload bind or use `echo` as proof of execution |
| Reddit commenters report `-dev` no longer skips intros and suggest `-novid` | Document `-novid` as an optional, unverified startup convenience for both launchers |
| The Reddit author describes 174 FPS as a personal sweet spot | Keep hardware-specific cap selection; do not adopt the comment's refresh-minus-one examples as universal targets |
| A Reddit user initially blames audio tweaks for stutter, then retracts that diagnosis | Do not claim audio tweaks caused or cured it; use repeatable before/after measurements |
| The Reddit author links telemetry to wireless input problems | Treat this as an unmeasured anecdote; leave telemetry and texture eviction overrides out of the baseline |
| GoodTechMaster recommends application-controlled AA/filtering and Auto threaded optimization | Retain those baseline choices |
| GoodTechMaster recommends High performance texture filtering for shooters | Keep it as an A/B option because motion shimmer and image quality also matter |
| GoodTechMaster describes FPS caps mainly as a power-saving tool | Also account for GPU headroom, frame pacing, and staying within the monitor's supported G-SYNC/FreeSync range |
| GoodTechMaster discusses driver Low Latency Mode without an Apex Reflex workflow | Prefer in-game Reflex; do not treat Ultra as an automatic FPS or smoothness improvement |
| GoodTechMaster suggests large shader caches | Keep the default unless cache pressure is identified; extra capacity does not guarantee fewer spikes |

The article also conflates NVIDIA Image Scaling with AI upscaling and describes a DirectX use for the driver's OpenGL triple-buffering control. Those explanations are not carried into this guide: NIS is spatial scaling/sharpening, and the Control Panel triple-buffering option is for OpenGL. DSR/DLDSR render above the chosen display resolution and can add substantial GPU work, so they are not part of the baseline. Driver availability and renderer support still determine whether a setting has any effect.

</details>

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

The repository retains its existing [GPL-3.0 license](LICENSE). Upstream-derived settings are credited in [notes](#notes), with the upstream MIT notice preserved in [third-party notices](#third-party).
