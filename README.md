# Ottl downloads

Public download home for **Ottl**, native macOS dictation with an axolotl
companion. The app itself is developed in a private repository; this one holds
only the signed, notarized builds and the download page.

- **Download page:** https://nsuder.github.io/ottl-releases/
- **All releases:** https://github.com/nsuder/ottl-releases/releases

Requirements: macOS 14 Sonoma or later. Every build is signed with a Developer
ID certificate and notarized by Apple, so it opens without warnings.

## Install

1. Open the `.dmg` and drag **Ottl** into **Applications**.
2. Open Ottl. Allow **Microphone** and **Speech Recognition** when asked.
3. Grant **Accessibility** (System Settings → Privacy & Security →
   Accessibility → Ottl), then quit and reopen Ottl.
4. Put the cursor in any text field, hold **fn**, speak, release.

## Early access

Current builds are for invited testers, who connect their own **AssemblyAI**
(speech) and **Groq** (cleanup, rewrite) accounts in Ottl → Settings. Keys stay
in the macOS Keychain. Without keys, Ottl uses Apple's on-device recognition.

## Verify a download

```bash
shasum -a 256 Ottl-<version>-<build>.dmg
```

Compare with the `.sha256` file attached to the same release.

## Publishing a release (maintainer notes)

From the private repository, after `scripts/release.sh` has produced
`dist/release/Ottl-<version>-<build>.dmg`, `.zip` and `.sha256`:

```bash
gh release create v<version> --repo nsuder/ottl-releases \
  --title "Ottl <version> (<build>)" --notes-file <notes.md> \
  dist/release/Ottl-<version>-<build>.dmg dist/release/Ottl-<version>-<build>.sha256
```

The download page reads the latest release from the GitHub API, so the button
updates by itself.
