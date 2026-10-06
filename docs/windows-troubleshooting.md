# Windows and PC troubleshooting

Start here when measurements show a problem. These are diagnostic steps, not an extra list of mandatory FPS tweaks for low-end PCs.

## Useful checks before advanced tweaks

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

## Windows Fast Startup versus BIOS Fast Boot

| Feature | What it changes | When to investigate |
| --- | --- | --- |
| Windows Fast Startup | Shutdown can save kernel/driver state for reuse on the next boot | A problem appears after Shut down → power on but disappears after Restart |
| BIOS/UEFI Fast Boot | Firmware may skip or shorten hardware initialization checks | USB/device detection, firmware access, or boot initialization problems |

Neither setting is a reliable general FPS or latency improvement once a healthy system is running. Low-end or midrange hardware alone is not a reason to disable either. They are separate settings; changing one does not necessarily change the other.

### Test Windows Fast Startup

First choose **Start → Power → Restart** and retest Apex. Restart performs a full Windows boot rather than using Fast Startup. If this consistently fixes a problem that returns after a shutdown/power-on cycle, test disabling Fast Startup:

1. Open **Control Panel → Hardware and Sound → Power Options**.
2. Select **Choose what the power buttons do**.
3. Select **Change settings that are currently unavailable**; Windows may require administrator approval.
4. Under Shutdown settings, untick **Turn on fast startup (recommended)** and choose **Save changes**.
5. Shut down, power on, and repeat the same test. Record whether it actually helps. Recheck the box to restore the previous behavior.

The option may be absent when hibernation is disabled or the system does not support it. Do not enable hibernation just to expose this checkbox. Disabling Fast Startup can lengthen boot time; it does not disable all BIOS fast-boot features.

### Test BIOS/UEFI Fast Boot only for a relevant problem

Use your motherboard or PC manufacturer's manual to find **Fast Boot / Ultra Fast Boot**. Record its original value, disable only that option, save, and test. Restore the original value if it makes no useful difference. Names and entry keys vary; Windows Advanced startup may also offer **UEFI Firmware Settings**.

Do not change Secure Boot, TPM, storage mode, or unrelated firmware settings as part of this test. Firmware updates and other hardware changes are separate troubleshooting decisions, not prerequisites for using this repository.

Use the [validation guide](validation.md) to separate a reproducible improvement from a single good match.

For O&O ShutUp10++, Winaero Tweaker, Autoruns, and measurement utilities, see [optional tools](optional-tools.md). These are optional diagnostic/customization choices, not prerequisites or guaranteed FPS improvements.
