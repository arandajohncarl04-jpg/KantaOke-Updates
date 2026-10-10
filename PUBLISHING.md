# KantaOke Public Update Channels

This repository publishes signed KantaOke APK updates, **not** the source code,
private signing keystore, or GitHub Actions credentials.

## Channels
- [Stable](channels/stable.json) — tested builds
- [Beta](channels/beta.json) — closed/open beta builds
- [Developer](channels/developer.json) — experimental builds

Until an APK is published, each channel contains `"release": null`.
Apps display "No published release" rather than a misleading success.

## How to publish a release

1. Build and test a new KantaOke APK in the **private** source repository.
2. Confirm it uses the same permanent signing key and Android package
   `dev.karaokemidilab.app`, with an increased Android versionCode.
3. Publish the approved signed APK as a **public GitHub Release asset** in
   this repository, e.g. a tag `v1.0.2-beta.3`. Do not publish unverified APKs.
4. Compute the SHA-256 of the exact signed APK and record its byte size.
5. Update the appropriate channel JSON to this schema:

```json
{
  "schema": 1,
  "channel": "beta",
  "release": {
    "versionCode": 44,
    "versionName": "1.0.2 - Third Closed Release",
    "apkUrl": "https://github.com/arandajohncarl04-jpg/KantaOke-Updates/releases/download/v1.0.2-beta.3/KantaOke-v1.0.2-beta.3-signed.apk",
    "sha256": "<64-character lowercase SHA-256 hex of exact signed APK>",
    "sizeBytes": 6500000,
    "notes": "Lyrics background/resume fix and public Update Center."
  }
}
```

The URLs and checksums above are *examples*, not real releases; never
publish a made-up SHA-256 or APK URL.

Only `https://github.com/arandajohncarl04-jpg/KantaOke-Updates/releases/download/`
URLs are allowed by the app; the app also verifies the signed APK's
SHA-256, package ID, installed signing identity and versionCode before
offering Android installation. A release should never be described as
available until its APK asset is actually uploaded.

The APK download and Android installation are user-initiated; the
system installer will request user confirmation. App settings and data
are preserved on a valid package/signature-matching update.

## Automatic publish workflow (preferred)

The private KantaOke source repository's
`.github/workflows/build-closed-beta.yml` has a *manual approval* toggle:
`publish_beta`. A normal source push still produces a private signed build
without publishing it to the public update channel.

The project owner configures one fine-grained GitHub token **as a secret in
the PRIVATE source repository** named `KANTAOKE_UPDATES_TOKEN`:

- Resource owner: `arandajohncarl04-jpg`
- Selected repositories: `KantaOke-Updates` **only**
- Repository permissions: Contents → Read and write

Do not paste the token into a manifest, APK, issue or chat.
Then, in the PRIVATE repository's Actions tab, choose the
**KantaOke Closed Beta - Permanently Signed** workflow, select the active
development branch, and run it with `publish_beta = true` after approval.

That build performs the original scoring audio check, uses the permanent
PKCS12 signing key, verifies the resulting APK signature and original audio,
and **then** uploads the exact signed APK as a public GitHub Release asset.
Finally it writes the signed APK's SHA-256, size and real URL to
`channels/beta.json`. App users on the Beta channel can then discover the
update from KantaOke Settings. No user needs MediaFire.

Please test on a non-critical device first: this checks automated packaging
and update integrity, but does not guarantee bug-free runtime playback.
