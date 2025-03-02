---
title: Installing Windows
author: "Kal Sandbrook"
date: 2025-03-02
weight: 2
---
# Installing Windows
## Bypassing TPM and Secure Boot Checks
1. Press SHIFT+F10 to open command prompt.
2. Open regedit, and navigate to `HKEY_LOCAL_MACHINE\SYSTEM\Setup`
3. Ceate a registry key called `LabConfig`
4. Create the `DWORD` values `BypassTPMCheck` and `BypassSecureBootCheck`, setting each to `1`.
5. Close regedit and command prompt, then continue installation.

## Installation steps
1. Select "English (World)" as Time/Currency format. Then after install, set the correct region in control.exe and ms-settings.

{{% hint info %}}
**Why?**

English (World) is not a valid region for the MS Store, meaning that a considerable amount of its features are disabled by default. Generally, the MS Store isn't a problem if you're using an **LTSC** build, but this is worth doing regardless.

{{% /hint %}}

2. Select "I don't have a product key"

3. When choosing an edition, pick the first occuring option from this list:
    - IoT LTSC
    - LTSC
    - Education
    - Home, Pro, literally any other option.
4. At installation type, *always* choose **Custom Install**. It's important to let windows take an entire drive first, then to shrink it after installation.
{{% hint info %}}
**Why?**

This is because Windows creates a 500MB recovery partition at the end of it's primary partition. It's much easier to deal with partitions that are at either end of the drive, rather than in the middle.

{{% /hint %}}

## Microsoft Login

{{% tabs "ms-login" %}}
{{% tab "Easy" %}}

1. Click on "Domain join instead" or equivalent
2. Easy.

{{% /tab %}}
{{% tab "Harder" %}}

1. On the "choose a country" screen, open command prompt.
2. Type `OOBE\BYPASSNRO` and wait for the computer to reboot
3. Then, re-open command prompt, and type `ipconfig /release` to temporarily disconnect from the internet.
4. Continue with installation, then click on the "I don't have internet" option when prompted to connect.
5. Then, "continue with limited setup"

{{% /tab %}}
{{% /tabs %}}

## Activation

1. Open up powershell, and run `irm https://get.activated.win | iex`.

### Installing and activating MS Office

1. Download office from [here](https://officecdn.microsoft.com/db/492350f6-3a01-4f97-b9c0-c7c6ddf67d60/media/en-us/ProPlus2021Retail.img).
2. Activate office using [massgrave](https://github.com/massgravel/Microsoft-Activation-Scripts)

## Post-install Clean-up

### Drivers
#### Graphics Drivers

{{% tabs "gpu drivers" %}}
{{% tab "AMD" %}}

1. Go to [AMD's website for downloading drivers](https://www.amd.com/en/support/download/drivers.html).
2. Scroll down to `Search or Browse Drivers and Support by Product`.
3. Manually search for your GPU (as well as CPU), then click submit.
4. Download the given drivers and install them.
    - **NOTE:** Adrenalin Edition is designed for general consumers; Pro Edition is designed for digital creative work.
    
    
Optional: [Radeon Software Slimmer](https://github.com/GSDragoon/RadeonSoftwareSlimmer), to reduce some of the bloat installed with AMD Drivers.

{{% /tab %}}
{{% tab "NVIDIA" %}}

1. Ensure all NVIDIA Drivers are uninstalled using DDU.
2. Find, download, and run NVCLeanstall.
3. Follow the given instructions, ensure that `Disable Installer Telemetry & Advertising` and `Perform a Clean Installation` are selected.

{{% /tab %}}
{{% /tabs %}}

#### Other Drivers

Other drivers can be found using a neat tool called [Snappy Driver Installer Origin](https://www.glenn.delahoy.com/snappy-driver-installer-origin/).

### Configuration

#### Settings

- Install cumulative & security updates.
- Configure Time & Language settings.
- Configure privacy settings.
- Set refresh rate.
- Disable Game Bar and Game Mode.
- Disable Core Isolation and Memory Integrity.
- Disable Hardware-accelerated GPU Scheduling.

#### Control Panel
- Configure power settings to nuke any performance-hindering power saving.
- Configure file explorer options.

#### Windows Features
- Disable unneeded windows features.

### Debloating

[privacy.sexy](https://privacy.sexy/) has some great scripts for enhancing privacy and debloating Windows.

The provided version of this script will disable a lot of features, but is relatively tame compared to the maximum settings. My preferred script can be found [here](https://linux.catsatnight.com/privacy-script.bat), and is only linked for convenience. Please review the contents of this file before running it.

### Customization

- [StartAllBack](https://www.startallback.com/) -- Modifies the start menu adn taskbar to be more useable.
- [Seleen-UI](https://github.com/eythaann/Seelen-UI) -- If you just fancy nuking everything and starting afresh.
- [Wox](https://github.com/Wox-launcher/Wox) -- A powerful launcher (alt + space) to enhance workflows.

## Fixing Linux dualboot

This guide assumes Linux has been installed *before* windows. Adapted from [this article](https://wiki.archlinux.org/title/Dual_boot_with_Windows)

### Prepwork
{{% hint danger %}}
**Be warned:**

Data loss can occur if Windows hibernates and you dual boot into another OS and make changes to files on a filesystem (such as NTFS) that can be read and written to by Windows and Linux, and that has been mounted by Windows. Windows may hibernate even when you press shutdown.

{{% /hint %}}

In order to mitigate this, you can disable both Fast Startup and Hibernation. Open an administrative command prompt, and enter:
```bat
powercfg /H off
```

### Process

1. Boot into a linux environment.
2. Mount the EFI partition and other relevant partitions.
3. chroot into your linux install, then run `grub-install` and other relevant setup instructions.
4. When generating the config for your bootloader, ensure that `osprober` is enabled.


## Accreditation

Much of the above information is adapted from those bastards on **/fwt/**, and those on the [Arch Wiki](https://wiki.archlinux.org/).
