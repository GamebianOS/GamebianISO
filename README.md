# Gamebian ISO downloads

Official **hybrid live/install ISO** images for [GamebianOS](https://github.com/GamebianOS/GamebianOS) — Debian tuned for a console-style gaming PC: install once with **Calamares**, finish **Steam** setup on the desktop, then boot into **gamescope + Steam Big Picture** like a Steam Deck.

This repository is for **end users** who want a ready-made image. To build from source, use the main [GamebianOS](https://github.com/GamebianOS/GamebianOS) tree (`Build/gambian-iso/`).

## Current release

| File | Size (approx.) | Base |
|------|----------------|------|
| **gamebian-1.0.0-amd64.iso** | ~2.3 GiB | Debian 13 (**trixie**), **amd64** |

> **Download:** This image is **too large for GitHub** (over the 2 GiB limit for git, LFS, and Releases). Download from the mirror link below (or torrent when available). This repo holds the README and checksums only.

| Mirror | Link |
|--------|------|
| *(add your host)* | `https://…/gamebian-1.0.0-amd64.iso` |

Release filenames use lowercase product name, [semantic version](https://semver.org/), and architecture. Add the Debian suite when it helps users tell releases apart, e.g. `gamebian-1.1.0-trixie-amd64.iso`. The live-build default artifact is `live-image-amd64.hybrid.iso`; rename when you publish to a mirror.

## System requirements

- **CPU:** 64-bit **x86_64 (amd64)** PC or laptop  
- **Firmware:** UEFI or legacy BIOS (hybrid ISO)  
- **RAM:** 8 GB minimum; 16 GB+ recommended for modern games  
- **Disk:** 32 GB+ free for installation (more for a game library)  
- **Network:** **Required during install** (Calamares downloads packages and runs post-install steps)  
- **GPU:** Vulkan-capable GPU recommended for gamescope; Steam can fall back to fullscreen X if gamescope is unavailable  

## Write a bootable USB

Use a USB stick **at least 4 GB**. **Back up anything on the stick — the whole device is erased.**

### Linux

Find the device name (e.g. `/dev/sdb`, **not** `/dev/sdb1`):

```bash
lsblk
```

Write the image (replace `sdX` and the ISO name):

```bash
sudo dd if=gamebian-1.0.0-amd64.iso of=/dev/sdX bs=4M status=progress oflag=sync
sudo sync
```

### Windows / macOS

- **[balenaEtcher](https://etcher.balena.io/)** — select the `.iso`, select the USB drive, Flash  
- **[Rufus](https://rufus.ie/)** (Windows) — choose the ISO; for a Debian hybrid image, use **DD mode** if Rufus asks  
- **[Ventoy](https://www.ventoy.net/)** — copy the `.iso` onto an already-prepared Ventoy USB (no per-image flash)  

Eject the USB safely before rebooting.

## Boot the live session

1. Plug in the USB and boot from it (BIOS/UEFI boot menu: often F12, F2, Esc, or Del).  
2. Disable **Secure Boot** if the firmware refuses to load the stick.  
3. The live system logs in automatically as user **`live`** (password **`live`**).  
4. You land on an **Openbox** desktop with the **Install Gamebian** installer (Calamares).  

Use the live session to check Wi‑Fi, display, and input before installing.

## Install to your machine

1. Open **Install Gamebian** (Calamares) if it is not already running.  
2. Connect to the **internet** — the installer requires it.  
3. Walk through the wizard: language, timezone, disk partitioning, and **create your user** (this becomes your everyday login).  
4. Wait for the copy and package steps to finish, then reboot and **remove the USB**.  

Calamares installs Gamebian to the target disk and removes the live-only `live` autologin account setup.

## After installation

| Step | What happens |
|------|----------------|
| **First boot** | LightDM autologins to **Openbox** (desktop mode). |
| **Steam setup** | A terminal walks you through installing/running **Steam**; sign in and quit Steam when done. |
| **Reboot or logout** | After sign-in, reboot or log out once. |
| **Everyday use** | Autologin into **gamescope + Steam Big Picture** (controller-friendly). Desktop mode stays available from the Steam menu or login screen. |

Optional: **gamebian-web** on port **8844** (`http://127.0.0.1:8844`) for ROM/library setup from another device on your LAN.

More detail (sessions, troubleshooting, controller menu): [GamebianOS build docs](https://github.com/GamebianOS/GamebianOS/blob/master/Build/README.md).

## Verify the download (optional)

If a `SHA256SUMS` file is published alongside the ISO:

```bash
sha256sum -c SHA256SUMS
```

## License

ISO contents are GPLv3 and other licenses from Debian and third-party packages. See [LICENSE](LICENSE).
