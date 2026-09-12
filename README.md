# AetherView

Public Ubuntu installers and signed application updates for the AetherView smart-meter desktop workbench.

**The application source code is private.** This repository contains release information and compiled installers only. It does not contain the private application repository, protocol source/codebooks, standard documents, build logs, or signing private keys. GitHub's automatically generated “Source code” archives contain only this public repository's files, not the private application source.

## Download

Get the current version from [Latest release](https://github.com/capriusbai/AetherView/releases/latest).

| Package | Use |
| --- | --- |
| `AetherView_VERSION_amd64.deb` | Recommended for Ubuntu users who prefer apt and application-menu integration. |
| `AetherView_VERSION_amd64.AppImage` | Portable alternative; keep it in a directory owned by your ordinary user. |

These are **Linux amd64/x86_64** packages, not ARM64 or iOS packages. The build and native no-hardware package checks use Ubuntu 22.04. Meter/device compatibility is a separate validation scope.

## Install

Download the chosen package and the release checksum file. To verify all four package/signature entries together, download both packages, both `.sig` files, and `SHA256SUMS.sha256`, then run:

```sh
sha256sum --check SHA256SUMS.sha256
```

Replace `VERSION` with the release version:

```sh
sudo apt install ./AetherView_VERSION_amd64.deb
# Start AetherView from the applications menu, or run:
aetherview-app
```

For AppImage:

```sh
chmod +x AetherView_VERSION_amd64.AppImage
./AetherView_VERSION_amd64.AppImage
```

If FUSE 2 is unavailable, the AppImage supports `--appimage-extract-and-run`. Do not run the GUI as root. Installation does not grant broad USB/serial permissions or alter meter firmware.

## Updates

The native application checks this repository on startup and every four hours, downloads a newer package, and verifies its signature against the embedded public key. Unverified packages are not installed. SHA-256 checksums alone are not a signature verification mechanism.

The update card offers installation after verification. Finish device connections and pending operations first. DEB updates require system administrator authorization; AppImage updates replace the user's original file. The application does not force a restart: the new version is used on the next normal launch.

Always install the current latest release. The initial `0.1.0` bootstrap used a two-minute package download deadline, which is too short for large AppImages on slow links; subsequent versions allow a separate, finite thirty-minute download budget. A `0.1.0` AppImage that cannot finish its update should be replaced manually with the latest AppImage.

Only signed binary release assets and the update manifest are published here. A release is not evidence of live meter calibration, firmware compatibility, or hardware acceptance.
