# 7-Zip for macOS

This fork of [7-Zip](https://github.com/ip7z/7zip) packages it as a native macOS app (`7-Zip.app`) with a Cocoa GUI, distributed as a `.dmg`. The app is a universal binary, so it runs natively on Apple Silicon (arm64) and on Intel Macs.

The macOS GUI comes from upstream pull request [ip7z/7zip#274](https://github.com/ip7z/7zip/pull/274) by [@Perzivall](https://github.com/Perzivall). This fork builds and ships it until it lands upstream. The compression engine is unchanged upstream 7-Zip code.

7-Zip website: [7-zip.org](https://7-zip.org)

## Features

- File manager window that shows folders and archives in one list, with toolbar buttons for Add, Extract, Test, Delete and Info
- Browse archives, including nested archives; add, delete and rename files inside them; drag and drop
- Add to Archive, Extract, Progress, Password, Overwrite and Properties windows with the same options as 7-Zip for Windows
- Finder services: Add to Archive, Compress to .7z / .zip, Open, Extract Files, Extract Here, Extract to Folder, Test Archive
- Translations from the standard 7-Zip `Lang/*.txt` files

## Install

1. Download `7-Zip-<version>-mac.dmg`. Get it from the latest successful **macOS GUI** run in this repo's [Actions](../../actions/workflows/macos-gui.yml) tab (the artifact is named `7-Zip-macOS`), or build it yourself (see below).
2. Open the DMG and drag **7-Zip** into **Applications**.
3. The app has an ad-hoc signature and isn't notarized, so the first time you open it, right-click it and choose **Open**. You can also use System Settings → Privacy & Security → **Open Anyway**.

Requires macOS 11 or later.

## Build from source

You need the Xcode Command Line Tools (`xcode-select --install`). You don't need an Xcode project.

```sh
# universal 7-Zip.app plus a DMG in CPP/7zip/Bundles/MacGUI/b/
CPP/7zip/Bundles/MacGUI/build_app.sh dmg

# or: build and install into /Applications, and register Finder services
CPP/7zip/Bundles/MacGUI/install_app.sh
```

To sign with a Developer ID, set `CODESIGN_IDENTITY` before you run `build_app.sh`. The full build notes are in [CPP/7zip/UI/MacOS/readme.txt](CPP/7zip/UI/MacOS/readme.txt).

## CI

The [`macOS GUI`](.github/workflows/macos-gui.yml) workflow builds the universal app on every push that changes `C/` or `CPP/`, checks it, and uploads the DMG as an artifact. You can also start it from the Actions tab.

## Keeping in sync with upstream

```sh
git fetch upstream
git merge upstream/main
```

## License

7-Zip is free software by Igor Pavlov, distributed under the GNU LGPL with the unRAR restriction. See [DOC/License.txt](DOC/License.txt).
