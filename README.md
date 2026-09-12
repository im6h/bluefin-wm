<div align="center">

# 🌊 nirifin

**An immutable, daily-built Wayland desktop powered by Niri, based on Bluefin & Bazzite.**

[![Build](https://github.com/im6h/nirifin/actions/workflows/build.yml/badge.svg)](https://github.com/im6h/nirifin/actions/workflows/build.yml)
[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](./LICENSE)
[![Image: GHCR](https://img.shields.io/badge/ghcr.io-im6h%2Fnirifin-blue?logo=github)](https://ghcr.io/im6h/nirifin)

</div>

---

## 📖 About

**nirifin** is a dual-base Linux distribution powered by [bootc](https://github.com/bootc-dev/bootc) and the [Universal Blue](https://universal-blue.org/) ecosystem. It offers pre-configured, atomic OS images that swap the traditional GNOME or KDE desktop for [Niri](https://github.com/YaLTeR/niri)—a modern, infinite-scrollable tiling Wayland compositor.

With daily automated builds ensuring you always have the latest security patches and upstream updates, `nirifin` provides a highly customized yet remarkably stable desktop experience.

### ✨ Key Pillars
- 🌀 **Scrollable Tiling**: Navigate windows on an infinite horizontal ribbon using Niri, augmented by the [Noctalia](https://github.com/noctalia-dev/noctalia) desktop shell.
- 🛡️ **Daily Security & Atomic Upgrades**: Images are rebuilt daily (`cron: "05 10 * * *"`) pulling the latest upstream updates and packages. Updates apply atomically in the background.
- 🎮 **Workstation & Gaming Flavors**: Choose the base that fits your workflow.
- 🇻🇳 **Vietnamese Input**: Out-of-the-box support via `fcitx5-lotus`, automatically tracking the latest GitHub releases during the image build.
- ⚡ **Curated Wayland Toolstack**: Ships with essential tools like Ghostty, Waybar, Rofi-Wayland/Fuzzel, SwayNC, Thunar, and more.

---

## 💿 Flavors & Rebase Guide

We provide two distinct flavors based on your needs:

| Flavor | Target Audience | Base Image | Command to Switch |
|---|---|---|---|
| **`nirifin`** | Developers & Workstations | [Bluefin-DX](https://projectbluefin.io/) | `sudo bootc switch ghcr.io/im6h/nirifin:latest` |
| **`nirizite`** | Gamers & Multimedia | [Bazzite](https://bazzite.gg/) | `sudo bootc switch ghcr.io/im6h/nirizite:latest` |

> [!WARNING]
> Switching your image via `bootc switch` will replace your current OS base. Your home directory (`~`) and `/etc` are preserved. Always back up important data before rebasing.

### Switch back / Rollback
To revert to your previous image at any time:
```bash
sudo bootc rollback
```

---

## 🪟 Niri & Noctalia

[**Niri**](https://github.com/YaLTeR/niri) abandons the standard grid layout for a scrollable horizontal workspace. Windows never shrink uncontrollably; instead, they tile into columns that you can scroll through effortlessly.

To make the system immediately usable, `nirifin` pairs Niri with **Noctalia**, a dedicated desktop shell providing:
- An integrated status bar
- Launcher / app switcher
- Native workspace overview for the scrolling layout

---

## 🇻🇳 Vietnamese Input Configuration

The image ships with [**fcitx5-lotus**](https://github.com/LotusInputMethod/fcitx5-lotus), compiled directly from the latest release for your Fedora base.

**Post-install setup:**
Add the following to `~/.config/environment.d/fcitx5.conf` (create if missing):
```ini
XMODIFIERS=@im=fcitx
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
SDL_IM_MODULE=fcitx
GLFW_IM_MODULE=ibus
```

Then launch **fcitx5-configtool**, add **Lotus**, and choose your preferred typing method (Telex / VNI / VIQR). Make sure to configure `fcitx5 &` to auto-start in your Niri configuration!

---

## 🏗️ Under the Hood

### Repository Structure
```text
nirifin/
├── Containerfile           # Image definitions pulling from uBlue bases
├── build_files/
│   └── build.sh            # Injects packages, configs, and COPR repos
├── system_files/           # System-wide overrides (/etc, /usr)
├── .github/workflows/
│   └── build.yml           # CI that builds images daily and on-push
└── image-template.env      # Build environment metadata
```

### Security & Signing
Images are built automatically by GitHub Actions and cryptographically signed using `cosign`. You can verify the integrity of any downloaded image using the public key `cosign.pub` included in this repository.

---

## 🤝 Community & Support

Built with ❤️ on top of [Universal Blue](https://universal-blue.org), [Bluefin](https://projectbluefin.io), and [Bazzite](https://bazzite.gg).

- 💬 [Universal Blue Forums](https://universal-blue.discourse.group/)
- 📖 [bootc Discussion](https://github.com/bootc-dev/bootc/discussions)
