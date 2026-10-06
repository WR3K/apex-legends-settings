# Choose settings for your PC

Use the limit you actually encounter, not a low-end/high-end label alone. The same GPU may be fast enough at 1080p and struggle with the same target at 1440p. A higher-priced PC can still stutter from heat, background work, or shader compilation.

## Find your specifications

- Press **Ctrl + Shift + Esc → Performance** in Task Manager. CPU shows the processor model; Memory shows installed RAM; GPU shows the graphics card and dedicated GPU memory. Shared GPU memory is not equivalent to dedicated VRAM.
- Open **Settings → System → Display → Advanced display**. Select your gaming monitor and confirm the resolution and refresh rate. Choose the intended supported refresh rate; a high-refresh screen can be left at 60 Hz accidentally.
- For NVIDIA, check **NVIDIA Control Panel → Set up G-SYNC**, if available, and your monitor's own Adaptive-Sync setting. A missing menu may depend on the display, connection, or GPU arrangement; do not assume all monitors support it.

## Pick a starting point

| Situation | First useful change | What to watch |
| --- | --- | --- |
| Entry-level GPU / limited VRAM | Low effects/shadows, modest texture budget; lower resolution if GPU limited | Texture pop-in, dedicated VRAM pressure, frame-time spikes |
| Balanced midrange system | Native resolution, low costly effects, sustainable cap, Reflex on NVIDIA | Busy-fight frame times and heat, not just range FPS |
| High-end GPU / high-refresh display | Start with the same baseline, then raise clarity settings with spare headroom | CPU limits, power/heat, and whether a higher cap stays stable |
| Laptop / integrated GPU | Use the proper power adapter and intended GPU; reduce resolution if needed | Thermal/power limits; integrated graphics share system RAM |
| High FPS but uneven motion | Compare a sustainable cap and, if available, the VRR profile | Cap overshoot, recurring spikes, tearing, shader warmup |

For texture budget, select a menu value below dedicated VRAM capacity with room for render targets and other assets. On an 8 GB card, a 4 GB budget is a reasonable initial comparison, not a requirement or a total-VRAM limit. Smaller cards should start lower. Raise it if memory headroom and measured results allow; selecting None is not automatically the smoothest option.

## Identify the bottleneck

A cap can make both CPU and GPU utilization low; that is normal. For a short controlled comparison, raise the cap above your observed FPS, keep other settings fixed, and compare two resolutions in the same scene. Restore the cap afterward.

- If lowering resolution noticeably improves FPS and the GPU was heavily loaded, rendering load is likely a limit. Reduce resolution or GPU-heavy settings first.
- If lowering resolution barely changes FPS, investigate CPU/game-thread load, other limits, temperatures, and background work. Overall CPU usage can look low while one critical thread is limiting performance.
- A utilization number alone is not a diagnosis. Record frame times and repeat the comparison after shader warmup.

Choose a cap your PC can usually sustain in demanding gameplay. There is no need to match monitor Hz exactly, and a cap cannot prevent every hitch. For VRR use the [presentation guide](../nvidia-settings.md); for G-SYNC off, a below-refresh cap does not itself prevent tearing.

## WR3K's current example

| Component / setting | User supplied |
| --- | --- |
| CPU | AMD Ryzen 7 5700X3D |
| GPU | NVIDIA GeForce RTX 3060 Ti |
| System RAM | 32 GB |
| Monitor refresh | 360 Hz |
| Resolution | Not yet supplied |
| G-SYNC | Off |
| FPS cap | 170, set in Steam launch options |

Keep the current cap as the comparison baseline:

```text
+exec autoexec.cfg +fps_max 170
```

Keep `fps_max` commented in autoexec and NVIDIA Max Frame Rate off. Your 170 FPS cap is valid on a 360 Hz monitor: it asks for a frame about every 5.88 ms, while the display refresh interval is about 2.78 ms. Those numbers are **not** total input latency, and fixed-refresh presentation can still tear or repeat frames unevenly. Do not switch to 357 FPS merely because the display is 360 Hz.

Start with in-game V-Sync off and Reflex Enabled. Compare Enabled + Boost while watching clocks and temperature. If 170 remains steady during demanding fights, compare a slightly higher target with identical captures; keep it only if pacing and responsiveness improve. If it repeatedly falls below 170, investigate the limiting component or try a lower cap. Resolution is still needed before recommending a more specific graphics target.

### What the supplied NVIDIA screenshots show

The screenshots show the Apex DX12 program profile, Fixed Refresh, highest available refresh, Low Latency Mode off, driver FPS cap off, V-Sync off, Prefer maximum performance, High performance texture filtering, sample/trilinear optimizations on, and Threaded optimization on. These are recorded settings, not measured improvements.

- Low Latency Mode off fits the proposed in-game Reflex workflow; the screenshot cannot confirm Reflex is enabled inside Apex.
- Keep your existing maximum-performance and texture-filtering choices as the baseline, then compare Normal power management and Quality filtering separately. Do not change several controls and attribute the result to one.
- Return Threaded optimization to Auto as a general default; forcing this OpenGL-oriented option on is not an established DX12 Apex improvement. OpenGL GDI compatibility is likewise not a useful Apex tuning target.
- Prefer application-controlled anisotropic filtering and antialiasing where supported, and choose their values in game. Controls marked unsupported for the application are not additional performance opportunities.
- The screenshot's “Highest available” setting does not prove Windows is currently using 360 Hz. Verify it in Advanced display.

Other readers should choose their own resolution, VRAM budget, cap, and presentation profile rather than copying this hardware example wholesale.
