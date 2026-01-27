# Non-Functional Requirements (A1)

## Platform support
- iOS/iPadOS: Latest major version only
- Devices: iPhone + iPad

## Data & sync
- All user content stored in SwiftData and syncs via iCloud (CloudKit-backed)
- Bundled decks are not stored in iCloud until duplicated

## Privacy
- No user accounts
- No analytics SDKs (MVP default: none)
- No tracking; no selling data
- Data stays in user iCloud container

## Accessibility (MVP baseline)
- Dynamic Type supported on key screens
- VoiceOver labels for main controls (Add, Save, Study actions)
- Tap targets meet Apple guidelines (baseline)

## Localization
- English only for MVP
