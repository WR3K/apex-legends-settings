# Steam launch options

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

If using the launch-option cap, leave `fps_max` commented out in the autoexec. Replace 141 for your display and measured performance; see [NVIDIA settings](nvidia-settings.md).

Do not add `-high`, `-threads`, old renderer flags, or network overrides as a default. They are not established improvements for your PC. A launch argument being accepted does not prove every autoexec command executed; follow [validation](docs/validation.md).

## Optional intro skipping

The supplied Reddit comments suggest `-novid` after reporting that `-dev` stopped skipping the intro. You may test:

```text
-novid +exec autoexec.cfg
```

This is a community-reported startup convenience, not a verified FPS or latency improvement. Keep your chosen cap if you already use one. If the current client ignores `-novid`, remove it; it is not required to load the autoexec.

## WR3K's current 170 FPS example

For the supplied 5700X3D / RTX 3060 Ti / 360 Hz setup with G-SYNC off:

```text
+exec autoexec.cfg +fps_max 170
```

This preserves the existing Steam cap; it is not a default for every reader. See the [hardware guide](docs/hardware-guide.md) before changing it. For help finding folders or saving the file in Notepad, use the [beginner walkthrough](docs/beginners.md).
