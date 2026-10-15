# KantaOke Remote OTA Channels

These manifests are for the **separate KantaOke Remote Android application** only.
They do not change the main KantaOke Universal Karaoke App manifests
in `channels/stable.json`, `channels/beta.json`, and `channels/developer.json`.

| Channel | Public manifest |
| --- | --- |
| Stable | [stable.json](stable.json) |
| Beta | [beta.json](beta.json) |
| Developer | [developer.json](developer.json) |

Manifest URLs (raw GitHub):

- https://raw.githubusercontent.com/arandajohncarl04-jpg/KantaOke-Updates/main/channels/remote/stable.json
- https://raw.githubusercontent.com/arandajohncarl04-jpg/KantaOke-Updates/main/channels/remote/beta.json
- https://raw.githubusercontent.com/arandajohncarl04-jpg/KantaOke-Updates/main/channels/remote/developer.json

The Remote app ID is permanently `dev.kantaoke.remote.v1047` (the version-looking
suffix is part of the **fixed package ID**, not an upgradeable version).

Each manifest is initialized with `release: null`. **That is intentional**:
creating an update channel does not automatically publish the user's private signed APK.
Publishing is a separate owner-approved operation in the private Remote repository
using the `Publish Signed KantaOke Remote OTA (Manual Approval)` workflow.
Only its selected Remote channel manifest is changed, *after* a public signed release
asset has been uploaded and verified with SHA-256.

When published, the release uses schema 1 and includes `versionCode`,
`versionName`, `apkUrl`, `sha256`, `sizeBytes`, and `notes`, matching the
basic main-app update manifest shape.

Important limitations:

1. The initial v1.04.7 compiled Remote is debug-signed in older installations.
   Moving to the new permanent key is a **one-time uninstall/reinstall**, not an
   in-place update. Back up pairing/settings before uninstalling.
2. The tested permanently signed v1.04.7 APK is Android `versionCode=14`.
   Its future in-place updates must keep the same application ID and signing key,
   and increment versionCode to at least 15.
3. The original Remote v1.04.7 *editable Android project is not yet recovered*.
   These **server-side manifests do not add an in-app Update Center** to the
   compiled Remote APK. Remote app-side update checks, download prompts,
   hash verification, and user-confirmed APK installation must be implemented
   and tested in a newer signed Android build. No silent installation is promised.
4. Beta/developer users may switch to Stable only when the Stable versionCode is
   newer than their installed build; Android normally rejects version downgrades.
5. Keep signing keys and source APKs out of this public repository.
