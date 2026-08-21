# PR Centre

PR Centre is a desktop workspace for academic research. It keeps literature, PDFs, notes, annotations, and working files together around each research project.

## What It Does

- Organizes research around projects.
- Maintains a reusable Library/Database of BibTeX entries and linked resources.
- Opens PDFs in an integrated Reader with search and reading controls.
- Sends quotations, screenshots, and source references from the Reader into project notes.
- Supports structured notes with text, citations, images, drawings, tags, and captions.
- Keeps rich-text and plain-text working files inside each project.
- Provides a Project Agent that can work with bounded project context and approved tools.
- Formats and copies references using preset or custom citation layouts.

## Main Areas

### Projects

Projects are the main research workspace. Each project brings together selected literature, reading material, notes, annotations, and files for one topic.

### Library/Database

The Library/Database stores bibliography entries and linked resources such as PDFs, folders, and URLs. The same literature entry can be reused across projects.

### Reader

The Reader provides PDF navigation, search, annotations, screenshots, and links back to the exact reading source.

### Notes and Files

Notes capture structured research material. Project Files support longer writing, rich-text documents, plain-text formats, and PDF export.

### Project Agent

The Project Agent can answer questions using approved project context and can use bounded File and terminal tools when explicitly authorized.

## Releases

Official builds are available from [GitHub Releases](../../releases). Version and asset metadata are recorded in [`versions.yml`](versions.yml).

## Release List

| Version | Platform | Architecture | Asset | Status |
| --- | --- | --- | --- | --- |
| `0.2.2` | macOS | `arm64` | [encrypted DMG](../../releases/tag/v0.2.2) | internal testing |
| `0.2.1` | macOS | `arm64` | [encrypted DMG](../../releases/tag/v0.2.1) | internal testing |

The current release is provided for macOS on Apple Silicon (`arm64`) as an AES-256 encrypted DMG. The password is distributed separately to invited testers.

## Recommended Download

Browser downloads can mark unsigned internal-testing apps with macOS quarantine metadata. For testers who are comfortable using Terminal, downloading with `curl` or `wget` is usually smoother and keeps the download flow close to PR Centre's in-app updater.

### macOS Apple Silicon

Copy and run this block in Terminal. It reads the latest version from `versions.yml`, downloads that release, and opens the DMG:

```bash
REPO="https://github.com/SinuoZhang/PR-Centre-Releases"
VERSION="$(curl -fsSL "https://raw.githubusercontent.com/SinuoZhang/PR-Centre-Releases/main/versions.yml" | ruby -ryaml -e 'puts YAML.safe_load(STDIN.read).fetch("latest")')"
FILE="PR-Centre-${VERSION#v}-arm64-encrypted.dmg"
curl -fL "$REPO/releases/download/$VERSION/$FILE" -o "$HOME/Downloads/$FILE"
open "$HOME/Downloads/$FILE"
```

Optional checksum check:

```bash
shasum -a 256 "$HOME/Downloads/$FILE"
```

Compare the result with the latest asset's `sha256` in [`versions.yml`](versions.yml). PR Centre's in-app updater performs this comparison automatically.

If `wget` is preferred, replace the download line with `wget -O "$HOME/Downloads/$FILE" "$REPO/releases/download/$VERSION/$FILE"`.

### Linux

Linux builds are not published yet. Future Linux releases will use the same latest-version pattern with the Linux asset name and package format listed in `versions.yml`.

## Installation Notes

Current macOS builds are ad-hoc signed for internal testing, but they are not Developer ID signed and not notarized. macOS may still display a security warning when opening the application.

PR Centre is currently closed-source and shared with selected testers by invitation. The application source and private research data are not stored in this repository.
