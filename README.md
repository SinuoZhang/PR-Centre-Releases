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
| `0.2.1` | macOS | `arm64` | encrypted DMG | internal testing, ad-hoc signed, not notarized |

The current release is provided for macOS on Apple Silicon (`arm64`) as an AES-256 encrypted DMG. The password is distributed separately to invited testers.

## Recommended Download

Browser downloads can mark unsigned internal-testing apps with macOS quarantine metadata. For testers who are comfortable using Terminal, downloading with `curl` or `wget` is usually smoother and keeps the download flow close to PR Centre's in-app updater.

### macOS Apple Silicon

Copy and run this block in Terminal:

```bash
RELEASE_MANIFEST="https://raw.githubusercontent.com/SinuoZhang/PR-Centre-Releases/main/versions.yml"
DOWNLOAD_DIR="$HOME/Downloads/prc-release"
REQUESTED_PLATFORM="macos"
REQUESTED_ARCHITECTURE="arm64"
REQUESTED_FORMAT="dmg"
mkdir -p "$DOWNLOAD_DIR"

MANIFEST_FILE="$DOWNLOAD_DIR/versions.yml"
curl -fsSL "$RELEASE_MANIFEST" -o "$MANIFEST_FILE"

LATEST_TAG="$(ruby -ryaml -e 'puts YAML.safe_load_file(ARGV[0]).fetch("latest")' "$MANIFEST_FILE")"

DOWNLOAD_URL="$(ruby -ryaml -e '
data = YAML.safe_load_file(ARGV[0])
latest = ARGV[1]
platform = ARGV[2]
architecture = ARGV[3]
format = ARGV[4]
release = data.fetch("releases").find { |item| item["tag"] == latest }
asset = release.fetch("assets").find { |item| item["platform"] == platform && item["architecture"] == architecture && item["format"] == format }
puts asset.fetch("downloadUrl")
' "$MANIFEST_FILE" "$LATEST_TAG" "$REQUESTED_PLATFORM" "$REQUESTED_ARCHITECTURE" "$REQUESTED_FORMAT")"

ASSET_NAME="$(basename "$DOWNLOAD_URL")"
curl -L "$DOWNLOAD_URL" -o "$DOWNLOAD_DIR/$ASSET_NAME"

EXPECTED_SHA256="$(ruby -ryaml -e '
data = YAML.safe_load_file(ARGV[0])
latest = ARGV[1]
platform = ARGV[2]
architecture = ARGV[3]
format = ARGV[4]
release = data.fetch("releases").find { |item| item["tag"] == latest }
asset = release.fetch("assets").find { |item| item["platform"] == platform && item["architecture"] == architecture && item["format"] == format }
puts asset.fetch("sha256")
' "$MANIFEST_FILE" "$LATEST_TAG" "$REQUESTED_PLATFORM" "$REQUESTED_ARCHITECTURE" "$REQUESTED_FORMAT")"

ACTUAL_SHA256="$(ruby -rdigest -e 'puts Digest::SHA256.file(ARGV[0]).hexdigest' "$DOWNLOAD_DIR/$ASSET_NAME")"
test "$ACTUAL_SHA256" = "$EXPECTED_SHA256" || { echo "SHA256 verification failed"; exit 1; }

open "$DOWNLOAD_DIR/$ASSET_NAME"
```

If `wget` is preferred, replace the two `curl` download lines with:

```bash
wget -O "$MANIFEST_FILE" "$RELEASE_MANIFEST"
wget -O "$DOWNLOAD_DIR/$ASSET_NAME" "$DOWNLOAD_URL"
```

### Linux

Linux builds are not published yet. Future Linux assets will use the same `versions.yml` manifest and the same pattern. When a Linux build exists, use the same block above with Linux values, for example `REQUESTED_PLATFORM="linux"`, the matching architecture, and the published package format.

## Installation Notes

Current macOS builds are ad-hoc signed for internal testing, but they are not Developer ID signed and not notarized. macOS may still display a security warning when opening the application.

PR Centre is currently closed-source and shared with selected testers by invitation. The application source and private research data are not stored in this repository.
