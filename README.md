# PR Centre Releases

This is the official binary release repository for **PR Centre**.

PR Centre is currently closed-source and under internal testing and development. The application source code is maintained in a separate private repository and is not hosted here.

Downloadable builds will be published through [GitHub Releases](../../releases) rather than committed to this repository. During the unsigned testing stage, each real release will use a semantic version tag such as `v0.1.0` and provide its DMG as a release asset.

The intended manual release flow is:

```text
Build PR Centre
-> generate DMG
-> create a version tag
-> create a GitHub Release
-> attach the DMG
-> write release notes
```

In the future, this repository may also serve as PR Centre's update source. Signed releases may include DMG, macOS ZIP, blockmap, and `latest-mac.yml` files as GitHub Release Assets, never as files in the normal Git repository tree.

No release is published until a real distributable build is available.
