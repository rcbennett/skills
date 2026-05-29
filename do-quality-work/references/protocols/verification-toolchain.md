# Protocol: Verification Toolchain — What I Can Test Without Rob

**Principle:** Confidence in changes comes from running them. Atlas should test as much as possible without waiting on Rob. Where I can't, I say so plainly and propose what Rob would need to do to close the gap.

## Currently working

| Surface | Command | Where | Speed | Notes |
|---|---|---|---|---|
| Cloud Functions TypeScript build | `npm run build` | `CloudFunctions/` | ~1.5s | Catches type errors and import errors immediately |
| Cloud Functions tests | `npm test` | `CloudFunctions/` | ~12ms (87 passing as of 2aadd17) | Mocha/chai; logic, role utils, content moderation, tracing, tvPairingV2 |
| Web admin tests | `npm test` | `PlatformClients/web/admin/` | ~26ms (98 passing) | Mocha/chai; XSS escape, renderers, isAdmin, capability taxonomy |
| Apple macOS app build | `xcodebuild build -scheme TerraFlo-macOS -destination 'platform=macOS'` | `PlatformClients/apple/` | minutes | Last verified 2026-04-24; Firebase package warning only |
| Apple iOS app build | `xcodebuild build -scheme TerraFlo-iOS -destination 'generic/platform=iOS'` | `PlatformClients/apple/` | minutes | Last verified 2026-04-24; existing Swift concurrency / MapKit warnings |
| Apple tvOS app build | `xcodebuild build -scheme TerraFlo-tvOS -destination 'generic/platform=tvOS'` | `PlatformClients/apple/` | minutes | Last verified 2026-04-24; existing Swift concurrency warnings |
| Android app build | `./gradlew :app:assembleDebug` | `PlatformClients/android/` | tens of seconds | Last verified 2026-04-24; SDK XML/deprecated icon warnings only |
| SharedCore (KMP) tests | `./gradlew test --quiet` | `SharedCore/` | ~16s | TCXExporter, Project, GPMF, TelemetryManager, TCRParser |
| TerraFloShared XCTest | `xcodebuild -scheme TerraFloSharedTests -destination 'platform=iOS Simulator,name=iPhone 17 Pro,OS=26.2' test` | `PlatformClients/apple/` | ~33s clean; faster incremental | Last verified 2026-04-21: 250 tests, 0 failures. Shared XCTest path for `TerraFloShared`; builds TerraFloShared + Firebase + nanopb cleanly on clean state. |

After any change to:
- `CloudFunctions/src/**/*.ts` → run `npm run build && npm test` in `CloudFunctions/`.
- `PlatformClients/web/admin/**/*.js` → run `npm test` in `PlatformClients/web/admin/`.
- `PlatformClients/apple/**/*.swift` → run the affected `xcodebuild build` scheme(s) from `PlatformClients/apple/`; run `xcodegen` first after adding/removing Swift files.
- `PlatformClients/android/app/**/*.kt` → run `./gradlew :app:assembleDebug` in `PlatformClients/android/`.
- `SharedCore/src/**/*.kt` → run `./gradlew test --quiet` in `SharedCore/`.

If a Storage rules change uses `firestore.get()` or `firestore.exists()`:
- Confirm the Firebase Storage service agent (`service-<project-number>@gcp-sa-firebasestorage.iam.gserviceaccount.com`) has `roles/firebaserules.firestoreServiceAgent`.
- If not, grant it before judging the deploy. Without that IAM binding, published asset reads will fail at runtime even if the rules compile and deploy cleanly.

If a callable or background function uses `admin.auth().createCustomToken(...)`:
- Confirm the deployed runtime service account has `roles/iam.serviceAccountTokenCreator` on itself.
- If not, grant it before judging pairing/auth flows. Without that IAM binding, the function will reach production and then fail at runtime with `iam.serviceAccounts.signBlob denied`.

## Currently blocked (needs Rob)

| Surface | Blocker |
|---|---|
| `xcodebuild -target TerraFloShared -destination 'iOS Simulator'` (no device name) | Reproducibly fails with the nanopb `build`-file conflict — turned out to be a diagnostic-only path, not a real workflow. **Use the scheme-based test command above instead** (`-scheme TerraFloSharedTests -destination 'platform=iOS Simulator,name=iPhone 17 Pro,OS=26.2'`) which does not hit this. |
| iOS / macOS app-level unit / UI tests | TerraFloShared XCTest exists, but app-layer XCTest and UI automation are still thin. Expanding that coverage is its own workstream. |
| On-device behavior — BLE, hardware, AirPlay, Photos picker | Requires real hardware Rob has and I don't. |

## Surface-by-surface escalation when blocked

When the primary build is unavailable:

- **Swift edit, build blocked:** I can't fully verify, but I can:
  - Use SourceKit diagnostics surfaced by the harness (note: imports of project frameworks like `TerraFloShared` / `FirebaseCore` will always be flagged as missing modules — that is an LSP limitation, not a real compile error).
  - Read the file end-to-end after editing; re-check syntax visually for the change.
  - Cross-check the public API surface used (`grep` for the symbol's definition).
  - Mark the commit body explicitly: "**Build verification blocked on DerivedData; fix is review-only until Rob clears.**" so Rob knows the diff didn't get a green light.

- **Cloud Functions / web edit, runtime blocked (e.g., emulator not configured):** unit tests run, integration is the gap; flag it.

- **KMP edit:** `./gradlew test` runs commonTest only. Platform integration on iOS/Android remains unverified until those build.

## Required practice

After every commit that touches a verifiable surface:
- Run the relevant test/build command **before** announcing the commit to Rob.
- If the command fails, **roll back the commit and investigate** before proceeding. Do not pile a fix-the-fix commit on top of a broken main.
- If the command succeeds, mention it in the message ("CloudFunctions tests still 70/70 green").

For Swift edits while builds are blocked:
- Acknowledge the gap in the commit body.
- Don't claim "verified" — claim "reviewed," and tell Rob a build is needed before merging conceptually.

## Atlas's role

- Pick the cheapest verification tool that exercises the change, and use it.
- When the change is too small for tests but the verification framework exists, still run `npm run build` (catches surprises in seconds).
- When verification is genuinely blocked, surface that explicitly to Rob in the commit / message, not silently.
- Periodically re-attempt currently-blocked surfaces (a fresh clone, an SDK install) and update this doc when a new path opens.

## How to add a new verification path

When a new test or build surface comes online (e.g., Rob clears DerivedData and Xcode builds work again):
1. Document the exact command, working directory, and expected runtime.
2. Add to the "Currently working" table in this doc.
3. From that commit forward, that path is required practice for changes touching that surface.
