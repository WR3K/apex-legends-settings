# Start here: files, Notepad, and common terms

You do not need to understand every setting to begin. Back up your files, make one change at a time, and test it. Use the in-game settings first; custom files are optional.

## What the terms mean

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

## Download this repository

On this repository's GitHub page, choose **Code → Download ZIP**. In File Explorer, right-click the downloaded ZIP → **Extract All**. Open the extracted folder. For a single file on GitHub, use its **Raw / Download raw file** control; saving the normal webpage can produce HTML instead of a config.

## Show filename extensions

Open File Explorer with **Windows + E**. On Windows 11 choose **View → Show → File name extensions**; on Windows 10 use **View → File name extensions**. This lets you distinguish `autoexec.cfg` from the incorrect `autoexec.cfg.txt`.

## Find the installed game files

**Steam:** Open Steam → **Library** → right-click **Apex Legends** → **Manage → Browse local files**. Alternatively use **Properties → Installed Files → Browse**. File Explorer opens the actual installation, even if you installed on a different drive. Open its **cfg** folder. This is where `autoexec.cfg` goes.

**EA app:** Open the Library, select Apex, and look for **Manage / View properties** and the installation location. Use **Browse** if offered, or open the displayed path in File Explorer. Labels vary by EA app version. Open the **cfg** folder inside that installation.

Do not guess a Steam drive letter or put the autoexec in the Windows Saved Games folder. If `cfg` is missing, first confirm you are in the folder containing the game's executable; create a folder named `cfg` there only if necessary.

## Find your saved video settings

1. Run Apex once, apply your preferred resolution, then close it normally.
2. Press **Windows + R** to open Run.
3. Paste the following path, including the percent signs, and press **Enter**:

```text
%USERPROFILE%\Saved Games\Respawn\Apex\local
```

4. Find `videoconfig.txt`. `%USERPROFILE%` expands to your Windows user folder; you do not need to type your username.
5. If the folder is missing, use **Windows + R → `shell:SavedGames`** and look for **Respawn → Apex → local**. Saved Games may have been relocated. Confirm you have launched Apex under this Windows account.

These are two different folders: the install's `cfg` folder holds the autoexec; Saved Games holds the video config.

## Back up and open files in Notepad

1. Close Apex. Copy each original file to a separate backup folder, such as `Documents\Apex-settings-backup`. Keep a screenshot or text copy of your existing launch options too.
2. Right-click the file → **Open with → Notepad**. Windows 11 may show **Show more options**, **Edit in Notepad**, or **Choose another app** first.
3. Edit only the intended lines. Preserve quotation marks and braces. Lines beginning with `//` in our autoexec are comments; they do not execute.
4. Press **Ctrl + S**. If saving fails, check the file's read-only attribute using the next section; do not change folder permissions blindly.
5. To create a new autoexec in Notepad, choose **File → Save As**, set **Save as type: All files**, and enter `autoexec.cfg`. Use UTF-8, then verify the final filename in File Explorer.

If an autoexec already exists, merge the wanted lines instead of overwriting binds and personal preferences. For video settings, follow the [merge guide](videoconfig.md): the repository's `videoconfig.txt` is deliberately incomplete and must not replace your full file.

## Optional: set or remove read-only

Leave the video config writable while choosing and testing settings. Once you have a known-good backup, read-only can help prevent ordinary writes to that file, but it is not required for this guide.

1. Close Apex and save the intended `videoconfig.txt` in Notepad.
2. In File Explorer, right-click **that file** → **Properties**.
3. On **General**, under **Attributes**, tick **Read-only**.
4. Click **Apply → OK**. To edit or save new permanent settings later, untick it and click **Apply → OK** first.

Use the file's checkbox, not the folder's checkbox. Do not mark the entire Apex folder read-only. An autoexec normally only needs to be read by the game; making it read-only is usually unnecessary.

### What happens if you Apply graphics settings in game?

**Read-only protects the file on disk; it does not lock live settings in the running game.** Pressing Apply can change graphics for the current session even if those values cannot be written to the read-only video config. A menu change can also supersede an overlapping value previously set by autoexec. This does not mean the game edited the autoexec itself.

On a full restart, Apex normally loads its saved settings and attempts to execute your startup autoexec again. Unsupported commands, loading order, other writable settings files, or cloud synchronization can affect the result, so read-only is not a guarantee that every setting will return exactly as expected. It also cannot make an unsupported command work.

For a permanent change: close the game, remove read-only, edit the relevant file or apply settings in game, exit normally, inspect the saved values, and test another launch. Re-enable read-only only if you still want it. Remove read-only before troubleshooting resolution changes or letting a game update migrate the config schema.

Continue with [in-game settings](../ingame.md), [choosing settings for your PC](hardware-guide.md), and [validation](validation.md).
