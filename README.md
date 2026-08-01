<div align="center">

# 🐟 bluefin-wm

**A custom [bootc](https://github.com/bootc-dev/bootc) OCI image built on [Bluefin](https://github.com/ublue-os/bluefin) —
curated for tiling window manager workflows with full Vietnamese input support.**

[![Build](https://github.com/im6h/bluefin-wm/actions/workflows/build.yml/badge.svg)](https://github.com/im6h/bluefin-wm/actions/workflows/build.yml)
[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](./LICENSE)
[![Image: GHCR](https://img.shields.io/badge/ghcr.io-im6h%2Fbluefin--wm-blue?logo=github)](https://ghcr.io/im6h/bluefin-wm)
[![ArtifactHub](https://img.shields.io/badge/ArtifactHub-bluefin--wm-blue?logo=artifacthub)](https://artifacthub.io)

</div>

---

## 📖 About

**bluefin-wm** is a customized, immutable Linux desktop image derived from [`ghcr.io/ublue-os/bluefin-dx`](https://github.com/ublue-os/bluefin). It is built using [bootc](https://github.com/bootc-dev/bootc) and published to the GitHub Container Registry (GHCR), ready to rebase onto any compatible Fedora Atomic system.

The image is designed for users who prefer a **Wayland tiling window manager** workflow over a traditional GNOME desktop, while retaining the stability and atomic update model of Universal Blue / Fedora Silverblue.

Key goals:
- 🪟 Ship **Niri** and **Hyprland** fully installed and ready to use
- 🇻🇳 Provide **Vietnamese input** out-of-the-box via [fcitx5-lotus](https://github.com/LotusInputMethod/fcitx5-lotus)
- 🎨 Include a curated Wayland toolstack (bars, launchers, notification daemons, theming tools)
- 📦 Keep everything reproducible, image-based, and atomic

---

## ✨ Features

### 🪟 Window Managers
| WM | Type | Description |
|---|---|---|
| [Niri](https://github.com/YaLTeR/niri) | Scrollable-tiling | A unique infinite-canvas scrolling compositor |
| [Hyprland](https://hyprland.org) | Dynamic-tiling | Feature-rich, highly configurable Wayland compositor |
| [Noctalia Shell](https://github.com/noctalia-dev/noctalia) | Desktop Shell | A cohesive Wayland desktop shell with bar, dock, notifications, and widgets |

### 🇻🇳 Vietnamese Input
- [fcitx5-lotus](https://github.com/LotusInputMethod/fcitx5-lotus) — automatically downloaded from GitHub Releases at image build time, matched to the running Fedora version (42 / 43 / 44+)

### 🛠️ Wayland Toolstack
| Category | Packages |
|---|---|
| Status bar | `waybar` |
| Launcher | `rofi-wayland`, `fuzzel` |
| Notifications | `swaync` (SwayNotificationCenter) |
| Wallpaper / Theming | `swww`, `matugen`, `wallust` |
| Screenshot | `grim`, `grimblast`, `slurp`, `swappy` |
| Clipboard | `cliphist`, `wl-clip-persist` |
| Terminals | `alacritty`, `kitty` |
| File manager | `thunar` + plugins |
| Bluetooth | `blueman`, `bluez`, `bluez-tools` |
| Audio | `pamixer`, `pavucontrol`, `playerctl`, `wireplumber` |
| Brightness | `brightnessctl` |
| Lock screen | `swaylock` (Niri), `hyprlock` (Hyprland) |
| Idle daemon | `hypridle` |
| Display control | `wlr-randr` |
| Qt theming | `qt5ct`, `qt6ct`, `kvantum`, `nwg-look` |
| XWayland bridge | `xwayland-satellite` |

### 🔡 Fonts
- `fira-code-fonts`
- `fontawesome-fonts-all`
- `google-noto-emoji-fonts`
- Pre-bundled from Bluefin: Adobe Source Code Pro, Droid Sans, Noto Sans CJK, JetBrains Mono, Symbols Nerd Font

---

## 🇻🇳 Vietnamese Input — fcitx5-lotus

This image ships [**fcitx5-lotus**](https://github.com/LotusInputMethod/fcitx5-lotus), a Vietnamese input method engine for [fcitx5](https://fcitx-im.org/).

### How it is installed

During the image build, `build.sh` automatically:
1. Queries the GitHub Releases API for the **latest** `fcitx5-lotus` tag
2. Selects the correct `.rpm` artifact for the current **Fedora version** (42 / 43 / 44 / rawhide)
3. Downloads and installs the package with `dnf5`

### Post-install setup

After rebasing to this image, configure fcitx5 as your input method framework by adding these environment variables to `~/.config/environment.d/fcitx5.conf` (create if it doesn't exist):

```ini
XMODIFIERS=@im=fcitx
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
SDL_IM_MODULE=fcitx
GLFW_IM_MODULE=ibus
```

Then open **fcitx5-configtool**, add **Lotus** as an input method, and set your preferred Vietnamese input scheme (Telex / VNI / VIQR).

> [!TIP]
> Run `fcitx5 &` from your WM startup config to auto-start the input daemon on login.

---

## 🪟 Window Managers

### Niri

[Niri](https://github.com/YaLTeR/niri) is a scrollable-tiling Wayland compositor. Instead of a traditional workspace grid, windows tile into infinite horizontal columns that you can scroll through.

**Packages installed:**

| Package | Purpose |
|---|---|
| `niri` | Compositor |
| `swaylock` | Lock screen |
| `noctalia-git` | Desktop shell — bar, launcher, and workspace overview for Niri |

#### Noctalia Shell

[**Noctalia**](https://github.com/noctalia) is a purpose-built desktop shell for Niri. It provides:
- A **status bar** (workspaces, system tray, clock, media)
- An integrated **launcher / app switcher**
- A **workspace overview** that fits naturally with Niri's scrollable layout

> [!NOTE]
> `noctalia-git` is built from the latest Git snapshot and sourced via the `errornointernet/packages` COPR repo.

### Hyprland

[Hyprland](https://hyprland.org) is a highly customizable dynamic tiling compositor known for smooth animations, rich IPC, and an active plugin ecosystem.

**Packages installed:**

| Package | Purpose |
|---|---|
| `hyprland` | Compositor |
| `hyprcursor` | Cursor theme manager |
| `hyprpaper` | Wallpaper daemon |
| `hypridle` | Idle / DPMS daemon |
| `hyprlock` | Lock screen |
| `hyprshot` | Screenshot utility |
| `hyprsunset` | Blue-light filter |
| `hyprutils` | Shared utility libraries |
| `xdg-desktop-portal-hyprland` | XDG portal backend |
| `hyprsysteminfo` | System info (Bluefin only) |
| `hyprpolkitagent` | Polkit agent (Bluefin only) |
| `hyprland-qt-support` | Qt integration (Bluefin only) |

> [!NOTE]
> `hyprsysteminfo`, `hyprpolkitagent`, and `hyprland-qt-support` are only installed on Bluefin (Qt 6.9). They are skipped on Bazzite due to a Qt version mismatch.

---

## 📦 COPR Repositories

The following [Fedora COPR](https://copr.fedorainfracloud.org/) repositories are enabled **during the image build** to source additional packages, then **disabled** in the final image to keep it clean:

| COPR Repo | Purpose |
|---|---|
| `eriker/SwayNotificationCenter` | `swaync` notification center |
| `errornointernet/packages` | Various Wayland utilities |
| `heus-sueh/packages` | `matugen`, `swww` (needed by hyprpanel) |
| `leloubil/wl-clip-persist` | Clipboard persistence across focus changes |
| `lionheartp/Hyprland` | Hyprland fix for Fedora 44 |
| `tofik/sway` | Sway-related tools |
| `ulysg/xwayland-satellite` | XWayland compatibility layer |
| `yalter/niri` | Niri compositor |

---

## 🚀 Installation

### Prerequisites

- A machine running a **bootc-compatible** image:
  - [Bluefin](https://projectbluefin.io) ✅ (recommended — same base)
  - [Bazzite](https://bazzite.gg), [Aurora](https://getaurora.dev), or [Fedora Silverblue](https://fedoraproject.org/silverblue/)
- Internet access for the initial rebase

### Rebase to `bluefin-wm`

```bash
sudo bootc switch ghcr.io/im6h/bluefin-wm:latest
```

Then **reboot**. On next login, select **Niri** or **Hyprland** from your display manager session list.

> [!WARNING]
> This will replace your current OS image. Your home directory and `/etc` are preserved. Make sure you have a backup of important data before switching.

### Verify current image

```bash
sudo bootc status
```

### Switch back / rollback

To revert to your previous image at any time:

```bash
sudo bootc rollback
```

---

## 📁 Repository Structure

```
bluefin-wm/
├── Containerfile           # Main image definition (FROM bluefin-dx)
├── build_files/
│   └── build.sh            # Package installation & customization script
├── system_files/           # System config files bundled into the image
│   ├── etc/                # /etc overrides
│   └── usr/                # /usr overrides
├── disk_config/            # ISO / disk image config (bootc-image-builder)
├── .github/workflows/
│   ├── build.yml           # CI: build & publish to GHCR
│   └── build-disk.yml      # CI: build ISO / QCOW2 / raw disk images
├── Justfile                # Developer tooling
├── image-template.env      # Image name, org, description, metadata
├── artifacthub-repo.yml    # ArtifactHub publisher verification
├── cosign.pub              # Public key for image signing verification
└── GUILD.md                # Full developer guide
```

---

## 🔧 Customizing

This image is built from the [Universal Blue image-template](https://github.com/ublue-os/image-template). To create your own fork:

1. Fork this repository
2. Edit `image-template.env` — set `IMAGE_NAME` and `REPO_ORGANIZATION`
3. Modify `build_files/build.sh` — add or remove packages
4. Add config files to `system_files/` — they are copied into the final image
5. Push — GitHub Actions will build and publish your image automatically

> [!IMPORTANT]
> Generate your own cosign key pair before pushing:
> ```bash
> COSIGN_PASSWORD="" cosign generate-key-pair
> gh secret set SIGNING_SECRET < cosign.key
> ```
> Never commit `cosign.key` to the repository.

---

## 🤝 Community

Need help, or want to share your config?

- 💬 [Universal Blue Forums](https://universal-blue.discourse.group/)
- 🎮 [Universal Blue Discord](https://discord.gg/WEu6BdFEtp)
- 📖 [bootc Discussion Forums](https://github.com/bootc-dev/bootc/discussions)

---

## 📜 License

This project is licensed under the **GNU General Public License v3.0**.
See [LICENSE](./LICENSE) for the full text.

---

<div align="center">

Built with ❤️ on top of [Universal Blue](https://universal-blue.org) · [Bluefin](https://projectbluefin.io) · [bootc](https://bootc.dev)

</div>
