# Ottl downloads

Public download home for **Ottl**, native macOS dictation with an axolotl
companion. The app itself is developed in a private repository; this one holds
only the signed, notarized builds and the download page.

- **Download page:** https://nsuder.github.io/ottl-releases/
- **All releases:** https://github.com/nsuder/ottl-releases/releases

Requirements: an Apple silicon Mac with macOS 14 Sonoma or later (Intel
support arrives with 0.1.61). US English only for now. Every build is signed with a Developer
ID certificate and notarized by Apple, so it opens without warnings.

## Install

1. Open the `.dmg` and drag **Ottl** into **Applications**.
2. Open Ottl and click **Enable dictation**; allow **Microphone** and
   **Speech Recognition** when macOS asks. If you clicked Don't Allow, turn Ottl
   on in System Settings → Privacy & Security → Microphone and → Speech
   Recognition.
3. Grant **Accessibility** (System Settings → Privacy & Security →
   Accessibility → Ottl), then quit and reopen Ottl.
4. Put the cursor in any text field, hold **fn**, speak, release. If fn also
   opens the emoji picker or Apple Dictation, set System Settings → Keyboard →
   *Press 🌐 key to* → **Do Nothing**.

## Early access

Current builds are for invited testers, who connect their own **AssemblyAI**
(speech) and **Groq** (cleanup, rewrite) accounts in Ottl → Settings. Keys stay
in the macOS Keychain. With Groq Whisper as the speech provider, the Groq key
alone is enough. Without keys, Ottl uses Apple's on-device recognition.

## Report a problem

[Open an issue](https://github.com/nsuder/ottl-releases/issues/new) with one
line about what happened and the *Last recording* and *Last delivery* lines from
Ottl → Settings → Diagnostics (they contain no dictated text). Issues are public.

## Verify a download

```bash
shasum -a 256 -c Ottl-<version>-<build>.sha256
```

Run it in the folder holding both the `.dmg` and the `.sha256` file from the
same release; it prints `OK`.

## Publishing a release (maintainer notes)

From the private repository, after `scripts/release.sh` has produced
`dist/release/Ottl-<version>-<build>.dmg`, `.zip` and `.sha256` (from 0.1.61
the `.sha256` lists only the DMG, by name):

```bash
gh release create v<version> --repo nsuder/ottl-releases \
  --title "Ottl <version> (<build>)" --notes-file <notes.md> \
  dist/release/Ottl-<version>-<build>.dmg dist/release/Ottl-<version>-<build>.sha256
```

The download page reads the latest release from the GitHub API, so the button
updates by itself.
