# KantaOke Updates

Official **public** APK update channels for KantaOke Universal Karaoke App.

The source code and permanent private signing keys remain in the private
development repository. Public GitHub Releases will contain only
owner-approved, permanently signed APKs.

See [publishing guide](PUBLISHING.md), [Stable](channels/stable.json),
[Beta](channels/beta.json), [Developer](channels/developer.json).

No APK is published until explicitly approved and uploaded.


## Separate KantaOke Remote update channels

The **KantaOke Remote** Android controller has independent manifests under
[channels/remote/](channels/remote/README.md): [Stable](channels/remote/stable.json),
[Beta](channels/remote/beta.json), and [Developer](channels/remote/developer.json).
These are separate from the main app's update channels. Remote releases are
owner-approved and use their own verified signing certificate and versionCode.
An empty `release: null` means no public Remote APK has been published yet.
