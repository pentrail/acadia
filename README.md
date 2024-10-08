# Acadia &nbsp; [![build-ublue](https://github.com/blue-build/template/actions/workflows/build.yml/badge.svg)](https://github.com/blue-build/template/actions/workflows/build.yml)

## What is this?
This is not a new linux distro, but rather a custom Fedora Atomic Image built using tools from [Universal Blue](https://universal-blue.org/) and [BlueBuild](https://blue-build.org/). You can think of it like a dotfile for a Fedora Atomic system. This image aims to provide the aesthetics of macOS and the functionality of GNOME in a Plasma 6 desktop. It also comes with basic productivity, development, gaming, and internet packages installed by default. 

## Screenshots
![Desktop](/screenshots/desktop.png)
![Dynamic Virtual Desktops](/screenshots/dynamic.png)
\* Accent color based on wallpaper

## Features
**Desktop:**
- Centered dock and top menu bar
- Dynamic virtual desktops (like GNOME)
- Super key opens overview (like GNOME)
- Searching in overview always opens new apps instead of searching existing ones (like GNOME)

**Applets:**
- Desktop Indicators (https://github.com/dhruv8sh/plasma6-desktop-indicator)
- USwitcher (https://gitlab.com/divinae/uswitch/)
- Application Title Bar (https://github.com/antroids/application-title-bar)
- Memory & CPU Usage Indicator

**Theming:**
- Transparency & Blur
- Accent Color & Slight Window Tint from Wallpaper
- MacSonoma Dark Plasma Theme (https://github.com/vinceliuice/MacSonoma-kde)
- Colloid Dark Icons (https://github.com/vinceliuice/Colloid-icon-theme)

**Preinstalled Packages:**
<details closed>
<summary>Flatpaks</summary>
  
- Discord
- KeePassXC
- OnlyOffice
- Kalk
- Kontact
- Okular
- Gwenview
- Elisa
- Kamoso
- Mpv
- Kdenlive
- Krita
- Blender
- Steam
- ProtonUp-QT
- Prism Launcher
- Github Desktop

</details>
<details closed>
<summary>RPMs</summary>

- [Upstream Packages](https://github.com/ublue-os/main/blob/main/packages.json)
- chromium
- code (VSCode)
- virt-manager
- libvirt
- virt-install
- edk2-ovmf
- qemu-kvm

</details>

## Installation

### Method 1. Fresh Install from a Release ISO (Recommended)
You can download a release ISO at https://www.adamwahid.com/acadia.

Checksums are available [here](https://github.com/pentrail/acadia/releases).

### Method 2. Fresh Install from a Generated ISO
You can generate an ISO of the latest image by following these instructions.
<details closed>
<summary>Acadia Main Installation</summary>
  
1. Install podman
2. Create a folder where the ISO should be stored:
```mkdir iso-output```
3. Generate ISO:
```sudo podman run --rm --privileged --volume ./iso-output:/build-container-installer/build --security-opt label=disable --pull=newer ghcr.io/jasonn3/build-container-installer:latest IMAGE_REPO=ghcr.io/pentrail IMAGE_NAME=acadia IMAGE_TAG=latest VARIANT=Kinoite```

</details>

<details closed>
<summary>Acadia Nvidia Installation</summary>
  
1. Install podman
2. Create a folder where the ISO should be stored:
```mkdir iso-output```
3. Generate ISO:
```sudo podman run --rm --privileged --volume ./iso-output:/build-container-installer/build --security-opt label=disable --pull=newer ghcr.io/jasonn3/build-container-installer:latest IMAGE_REPO=ghcr.io/pentrail IMAGE_NAME=acadia-nvidia IMAGE_TAG=latest VARIANT=Kinoite```

</details>

Detailed instructions are available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso).

### Method 3. Rebasing an existing Atomic install

> **Warning: This is not recommended because you will not get any of the desktop configuration and theming changes**  
> [This is also an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/pentrail/acadia:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/pentrail/acadia:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/pentrail/acadia
```

## Known Issues
- Digital clock may not render bold text.
`
Temporary Fix: Change the font weight in the applet settings to something else and apply, then return back to bold and apply.
`
