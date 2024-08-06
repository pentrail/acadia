# Acadia &nbsp; [![build-ublue](https://github.com/blue-build/template/actions/workflows/build.yml/badge.svg)](https://github.com/blue-build/template/actions/workflows/build.yml)

## What is this?
This is not a new linux distro, but rather a custom Fedora Atomic Image built using tools from [BlueBuild](https://blue-build.org/). You can think of it like a dotfile for an entire linux distribution. This image aims to provide the aesthetics of macOS and the functionality of GNOME in a KDE6 desktop. It also comes with basic productivity, development, gaming, and internet packages installed by default. 

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

**Preinstalled Applications:**
> Flatpaks: TODO

> RPMs: TODO

## Installation
You can generate an ISO by following these instructions.
1. Install podman
2. Create a folder where the ISO should be stored:
```mkdir iso-output```
3. Generate ISO:
```sudo podman run --rm --privileged --volume ./iso-output:/build-container-installer/build --security-opt label=disable --pull=newer ghcr.io/jasonn3/build-container-installer:latest IMAGE_REPO=ghcr.io/pentrail IMAGE_NAME=acadia IMAGE_TAG=latest VARIANT=Kinoite```

Detailed instructions are available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso).

## Rebasing an existing Atomic install

> **Warning: This is not reccomended because you will not get any of the desktop configuration and theming changes**  
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
