# TidyDesk 1.0.0 validation

Prepared 31 October 2026 (Australia/Melbourne). The release was approved by the owner for publication on GitHub.

## Build

- Public/free compilation using `Scripts/build-local.sh`, without `TIDYDESK_OWNER`.
- Apple Swift 6.4, installed macOS SDK, Apple Silicon build host.
- Version 1.0.0, build 5; bundle identifier `com.tidydesk.app`; deployment target macOS 14.0.
- Mach-O arm64 executable. Intel is not included in this release asset.
- App Sandbox, user-selected read/write access and app-scoped bookmarks retained; no network entitlement.
- Ad-hoc signature verified with `codesign --verify --deep --strict` both before packaging and after extracting the ZIP.
- Xcode project plist syntax passes `plutil -lint`. Full Xcode is not installed; no `xcodebuild`/Xcode archive validation was performed.

## Automated tests

All 39 tests in 4 suites passed in the release run. Tests create isolated temporary fixtures. Coverage includes read-only scanning, collision suffixes, a destination appearing after preview, partial failures, journal failures, relaunch recovery, Undo collisions, changed files, cancellation, custom destinations, matching and access policy.

The complete test output is in `TEST-RESULTS.txt`.

## Native app test

The actual public 1.0.0 app was launched and displayed its FREE tier. Using a newly created temporary directory only:

1. Created six loose synthetic files (one per category), a pre-existing `Documents/report.txt` duplicate and a nested file.
2. Recorded all eight original paths and SHA-256 hashes.
3. Chose that folder through the native picker. Scan showed six loose files and proposed `Documents/report (2).txt` for the duplicate.
4. Verified all eight paths/hashes were unchanged after scanning.
5. Selected the six files, reviewed the confirmation, then cancelled. Verified all eight original paths/hashes remained unchanged.
6. Explicitly confirmed the six test moves. Verified all six category destinations and content hashes; confirmed existing duplicate and nested file were unchanged.
7. Quit and relaunched the app. The saved Undo record and six moved destinations were restored.
8. Explicitly confirmed Undo. The UI reported “6 files restored · Undo complete”. All eight original file paths and hashes matched the initial manifest. Empty category directories remain as designed.
9. Extracted the final ZIP into a separate temporary directory, reverified the signature and successfully launched that extracted app.

No real Downloads, Desktop, STEM/STEAM or other personal files were moved by these checks. The private Owner app was not rebuilt or included.

## Packaging

The release ZIP contains only `TidyDesk.app` and its bundled resources/signature. Its embedded plist was checked for version 1.0.0 and the public bundle identifier. No Owner binding, private Owner app, temporary fixtures or recovery journal is included. `SHA256SUMS.txt` records the ZIP hash.

## Limits of this verification

This is local build/run verification, not Apple review or notarisation. It does not test a browser-downloaded/quarantined copy on another Mac, every supported OS version, Intel hardware or all filesystem/permission configurations. There is no Developer ID signature and no Apple notarisation ticket. Gatekeeper can block downloads. The README documents this limitation and the currently unavailable Pro activation.
