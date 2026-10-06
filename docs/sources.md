# Sources and implementation notes

Reference review: 2026-10-07. No local Apex runtime testing was available.

| Source | Use and access status |
| --- | --- |
| [DominicKlmNL/apex-legends-config](https://github.com/DominicKlmNL/apex-legends-config) | Inspected README, configs, launcher guides, in-game guide, NVIDIA guide, and MIT license at commit `5d5ab6a0c93c3a9169b9f3c6f2d10e85b245f2b3` |
| [Reddit post supplied by WR3K](https://www.reddit.com/r/apexlegends/comments/1w4ljsh/after_years_of_regularly_finetuning_my_pc_i/) | Reviewed the user-supplied transcript of the post and comments; direct retrieval returned HTTP 403. Community reports are not controlled benchmarks. |
| [GoodTechMaster NVIDIA guide](https://www.goodtechmaster.com/ultimate-guide-nvidia-control-panel-optimization-for-gaming/) | Reviewed the user-supplied article text, dated August 12, 2022; direct retrieval returned HTTP 403. General driver guidance, not current Apex-specific validation. |

The upstream author labels many commands as working. Those labels are upstream claims, not verification of this repository or the current client. This project matches the reference's main categories while curating its settings rather than mirroring every override.

## Deliberate differences

- Include `hud_setting_adsDof "0"`, already present upstream, as WR3K's requested ADS blur preference. Do not invent a generic `dof 0` command.
- Keep `mat_depthfeather_enable "0"` commented as a separate legacy experiment. Depth feathering is not interchangeable with ADS depth of field.
- Leave the frame cap for hardware-specific selection instead of imposing upstream's 174 FPS target.
- Provide a merge-only video config, retaining the user's display, VRAM budget, and client schema.
- Offer separate VRR/tear-free and tearing-allowed presentation profiles. Avoid claiming one fixed cap maximizes every performance goal.
- Prefer menu controls and a minimal autoexec. Omit unverified network/prediction, telemetry, threading, ragdoll, decal, and forced texture overrides from the active config.
- Preserve personal mouse, audio, binds, FOV, and gameplay preferences; do not force upstream's 7.1 audio layout or autosprint.
- Avoid mandatory read-only configs, high process priority, global driver changes, or routine cache deletion.
- Use `+exec` for both launcher guides and explicitly flag the upstream EA `-exec` discrepancy for on-PC validation.

These are conservative implementation choices, not benchmark findings. See [validation](validation.md) before claiming gains. Portions of the configuration are adapted from Downie2k's MIT-licensed work; the notice is retained in [THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md). The existing project license is unchanged.

## Findings from the supplied website text

The pasted text makes both previously inaccessible sources available for review. It does not establish that the live pages are unchanged or that their technical claims have been independently tested.

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
