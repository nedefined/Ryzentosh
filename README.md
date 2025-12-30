# Ryzentosh
It all started a year ago. That’s when I decided: since the hardware for macOS is perfect — it’s time to act. Since then, there have been countless attempts to get this system running... And finally, __on December 29, 2025__, I actually did **it**.

Specs: 
+ The main source of all my headaches, the **MSI B550M-Pro Gen 3** motherboard;
+ **AMD Ryzen 5 5600** (Zen 3);
+ **AMD RX 6600** (Navi 23);

# How to replicate:

> [!CAUTION]
> **UPDATE YOUR FIRMWARE FIRST**

When working with `config.plist`, you need to watch every single character, which means — stay absolutely sober.

1. Generate a clean and basic config via [OpCore-Simplify](https://github.com/lzhoang2801/OpCore-Simplify) (only essential kexts and SSDTs).
2. Open `config.plist` and pay close attention to:
   + ACPI : `Patch`
   + Kernel : `Patch`
   + NVRAM : `7B...` : `boot-args`
3. For our hardware, we need `SSDT-PLUG-ALT.aml` (CPUR), `SSDT-EC.aml` (FakeEC), and `SSDT-USBX.aml` (USBX). Dump them via [SSDTTime](https://github.com/corpnewt/SSDTTime), and **MANDATORY: apply the OpenCore patches from the results folder.**
4. Update all kexts to the latest version (VirtualSMC, Lilu, WhateverGreen, etc.).
5. Final check. Make sure all files in the OC folder are actually present in your config.

Reboot. Spam F11, pick the last item. Hit F6.

> [!NOTE]
> **SPECIFICALLY FOR OUR HARDWARE**

Disable:
+ `Fast Boot`
+ `Secure Boot`
+ `AMD fTPM`
+ Anything you don't particularly like (e.g., that MSI utility)

Enable:
+ `Re-size BAR...`
+ `Above 4G...`
+ Whatever you feel like (e.g., Smart Fan)

Using the USB drive you made following the [Dortania guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/windows-install.html), boot into Apple Recovery (DMG). Now:

If any errors pop up, identify the source, Google the error, post a screenshot in [issues](https://github.com/nedefined/Ryzentosh/issues), on [r/hackintosh](https://reddit.com/r/hackintosh), or in chats — ask for help.

> [!NOTE]
> **Navi 23, black screen after Verbose Mode: what do?**

### If you're sure the logs stopped at the very last moment and you're supposed to be in the installer, **OR** if your screen just went blank/turned off:

Go back to `boot-args` and delete `-v debug=0x100 keepsyms=1`! Now boot!

Next step: check for internet in Safari (**`ping` and `curl` in terminal don't count!**). If it's failing, grab the full .raw installer [from here](https://github.com/yusufklncc/Hackintosh-for-All-Computers) and write it to the USB via [Etcher](https://balena.io/etcher).

**Install the system, enjoy the system.**
