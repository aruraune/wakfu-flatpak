# WAKFU

Wakfu is a tactical turn-based MMORPG developed by Ankama Games and released for Microsoft Windows, macOS, and Linux on 29 February 2012.

This repo hosts an unofficial flatpak wrapper for [Wakfu](https://www.wakfu.com/en/mmorpg).

This wrapper extracts the official AppImage and starts the Ankama Launcher.

## Quick Install

```sh
git clone https://github.com/aruraune/wakfu-flatpak
cd wakfu-flatpak
flatpak-builder --user --install --force-clean build com.ankama.Wakfu.yaml
flatpak run com.ankama.Wakfu.yaml
```

## Create Flatpak Bundle

While this process is documented I opted to not distribute the bundle itself to avoid redistributing the Ankama Launcher installer.

```sh
flatpak-builder --force-clean build com.ankama.Wakfu.yaml
flatpak build-export export build
flatpak build-bundle export wakfu-flatpak.flatpak com.ankama.Wakfu --runtime-repo=https://flathub.org/repo/flathub.flatpakrepo
```

## Note

The official launcher may be updated over time. If you see this error:

```
Failed to download sources: module wakfu: Wrong sha256 checksum for Wakfu-Setup-x86_64.AppImage, expected "3c0d37befb89099b6c99dd32486d5b1c23c1d82921abcddc8002143259a086a0", was "<SHA256_HASH>".
```

Please edit `com.ankama.Wakfu.yaml` (line 42) and update the sha256 of the installer. There's an example below to show what exactly needs to be updated.

Feel free to open a merge request should you encounter this issue.

Before:
```yaml
    sources:
      - type: file
        dest-filename: Wakfu-Setup-x86_64.AppImage
        url: https://launcher.cdn.ankama.com/installers/production/Wakfu-Setup-x86_64.AppImage
        sha256: <something_invalid>
```

After:
```yaml
    sources:
      - type: file
        dest-filename: Wakfu-Setup-x86_64.AppImage
        url: https://launcher.cdn.ankama.com/installers/production/Wakfu-Setup-x86_64.AppImage
        sha256: 3c0d37befb89099b6c99dd32486d5b1c23c1d82921abcddc8002143259a086a0
```

## Legal

The Wakfu game and the Ankama Launcher are **proprietary** (closed source) applications.

This wrapper is not verified by, affiliated with, or supported by Ankama Games nor Ankama Studio.
