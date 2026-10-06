# EA app launch options

Find Apex's installation folder through the EA app's game properties/manage menu, then open `cfg`. Back up and merge any existing autoexec before installing [autoexec.cfg](autoexec.cfg).

In the game's properties, locate Advanced launch options (the label can vary with app versions), save your previous arguments, and enter:

```text
+exec autoexec.cfg
```

The `+exec` command is passed to the game engine. The upstream guide lists `-exec` for EA; that distinction is not verified here, so this guide uses the usual engine command syntax and requires an execution check on your installation.

An optional cap uses `+fps_max N`, with N replaced by your selected integer target. For example, `+exec autoexec.cfg +fps_max 141` is a 144 Hz VRR starting example, not a universal preset. Leave `fps_max` commented in autoexec if you set it here. See [NVIDIA settings](nvidia-settings.md) and [validation](docs/validation.md).

## Optional intro skipping

The supplied Reddit comments suggest `-novid` after reporting that `-dev` stopped skipping the intro. You may test:

```text
-novid +exec autoexec.cfg
```

This is a community-reported startup convenience, not a verified FPS or latency improvement. Keep your chosen cap if you already use one. If the current client ignores `-novid`, remove it; it is not required to load the autoexec.
