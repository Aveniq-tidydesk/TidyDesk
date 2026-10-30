# TidyDesk 1.0.0

A free, native macOS file organiser. Choose a folder, review where files will go, select what to move, and confirm. Everything stays on your Mac: no accounts, cloud services, analytics, payments, background monitoring or automatic organising.

## Download requirements

- macOS 14 Sonoma or later.
- Apple Silicon Mac (M1 or later). This ZIP does not contain an Intel build.
- Enough access to read and move the files in the folders you select.

**Warning: this app is not Apple-notarised.** It is signed locally with an ad-hoc signature, not an Apple Developer ID certificate. Apple has not reviewed this release or notarised it. macOS Gatekeeper may block it after downloading. A successful local launch does not guarantee that a downloaded copy will open on another Mac. Do not disable Gatekeeper or remove quarantine attributes to install it. If macOS blocks it, stop and use a source build you trust or wait for a Developer ID-signed, notarised release.

## Install

1. Download `TidyDesk-1.0.0-macOS-arm64.zip` from the release assets when a release is published.
2. Optionally check the download against `SHA256SUMS.txt` using `shasum -a 256 TidyDesk-1.0.0-macOS-arm64.zip`.
3. Double-click the ZIP in Finder to extract it.
4. Drag `TidyDesk.app` into Applications. If updating, finish or Undo any active organisation and quit TidyDesk first. Preserve the app's local data so its Undo record remains available.
5. Open TidyDesk. The notarisation warning above applies to downloaded copies.

Download the published release at https://github.com/Aveniq-tidydesk/TidyDesk/releases/tag/v1.0.0.

## First use

Start with a disposable sample folder, not your main Downloads folder. Keep a backup of valuable files.

1. Open **Tutorial** in the sidebar for a five-step practice using pretend files.
2. In **My files**, choose a folder. Scanning is read-only and nothing starts selected.
3. Check each proposed destination. Expand a row for full paths. The file-type filter shows category counts and sizes.
4. Select files, then click **Review moves…**. The default destinations are Documents, Images, Videos, Audio, Archives and Other inside the scanned folder.
5. Inspect the confirmation sheet and click **Confirm & move** only when ready. **Cancel** returns without moving files.
6. Use **Show in Finder** to locate moved files. Use **Undo…** and confirm to restore their original locations.

For a custom destination, use **Find similar** next to a reference file, review the suggested matches, then **Choose destination…**. These files move directly into the folder you choose. Additional filename/type matching choices are in the row's menu.

**Cancel operation** stops after the current file finishes. Completed moves retain Undo. **Keep moves…** leaves files in place and clears the saved Undo record so another batch can begin.

## Safety and privacy

- Existing files are never deliberately deleted or overwritten. Duplicate names receive a visible numbered suffix in the preview.
- A destination that becomes occupied after preview causes a safe failure instead of overwriting it.
- Failed files are reported and remain at their original locations. Partial success retains Undo for completed moves.
- One saved Undo batch survives relaunch. Changed files or occupied original paths are skipped, reported and retained for a retry.
- Folder access comes from the native macOS picker. Security bookmarks, local paths, metadata and the Undo journal are stored locally in the app's sandbox container. There is no network entitlement.
- TidyDesk is an organiser, not a backup system. Undo is conditional on access and unchanged files; it cannot reverse arbitrary edits by other apps or storage failures.

## Known limitations

- Scans only regular files directly inside the selected folder. Hidden files, nested folders, packages and symbolic links are skipped.
- Categories are based on filename extensions; unknown types go into Other.
- The free public edition supports related names, same filename stem and same extension matching. Content-aware image/document/media comparison is unavailable in this edition. Pro purchase/activation is not implemented; there is no payment required to use the available features.
- Matching is a suggestion, not a guarantee of related content. Always review the selection and destination.
- Cross-filesystem moves are unsupported; there is no copy-and-delete fallback.
- Only one active Undo batch is supported. Keep or Undo that batch before organising another.
- Undo leaves empty destination folders behind. Edited, moved or inaccessible files can prevent a complete Undo.
- Folder permissions may need reconnecting after relaunch. Reconnect the original folder and custom destination as prompted.
- Cancellation is cooperative and can wait for the current file or native decoding operation.
- No Intel binary is included. macOS 14 is the deployment target, but this release was tested on the build Mac rather than every supported macOS version.
- No automatic update service. Install future versions manually.
- This is an ad-hoc signed, non-notarised release candidate. Public download/Gatekeeper behaviour has not been verified on a separate Mac.

## Build from source

The source project is maintained separately from this binary ZIP. On a Mac with a Swift 6-capable Xcode/Command Line Tools installation and a compatible macOS SDK:

```sh
cd TidyDesk
./Scripts/test.sh
./Scripts/build-local.sh
```

The app is created at `.build/TidyDesk.app`. The script builds for the current Mac's architecture and signs locally. Full Xcode is required to open `TidyDesk.xcodeproj` or use `xcodebuild`; it is not required by the command-line build script. The supplied Xcode project has not been validated with full Xcode on this build machine.

Private Owner apps, generated identity bindings, test folders and recovery journals are excluded from the public ZIP. This is a free binary distribution; no open-source licence is granted by this README.

See `VALIDATION.md` for the checks performed for this release.
