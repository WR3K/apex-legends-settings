# NVIDIA settings and frame pacing

Use NVIDIA Control Panel → Manage 3D settings → **Program Settings**, then select the executable your Apex installation actually runs. Browse to it if necessary; do not assume a fixed DX11/DX12 executable name. Record existing settings first. These profiles are starting points requiring on-PC validation.

## Choose a presentation profile

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

## Driver baseline

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

## How the supplied NVIDIA article is used

The GoodTechMaster article is dated 2022. Its application-controlled AA/filtering and Auto threaded-optimization recommendations fit this baseline. High performance texture filtering and larger shader caches remain optional comparisons, not guaranteed improvements. Its general Low Latency Mode discussion does not replace an Apex-specific Reflex setup, and frame caps can help pacing and VRR operation as well as power consumption. See [source decisions](docs/sources.md) for the differences.

WR3K's supplied driver screenshots and current 170 FPS / G-SYNC-off configuration are discussed in the [hardware guide](docs/hardware-guide.md). Use that as a worked example, not a universal profile.
