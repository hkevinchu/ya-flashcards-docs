# Data Inventory & Data Flow Mapping (A6.1)

Last updated: 2026-01-20  
Owner: Kevin  
App: Flashcard iOS App (iPhone + iPad)

## Purpose
This document is the source of truth for what data the app collects, stores, and transmits. It is used to:
- Draft the Privacy Policy (A6.2)
- Prepare App Store Connect privacy questionnaire responses (A6.3)
- Keep disclosures aligned with actual app behavior

---

## Data Inventory (Authoritative)

| Data Category | Description | Source | Stored Where | Transmitted Off Device | Linked to User |
|-------------|------------|--------|--------------|------------------------|---------------|
| User Content | Flashcard decks, cards, folders/collections, ordering | User | On-device + iCloud | Apple iCloud only | Yes (Apple ID) |
| Study State | In-session progress, card order, remaining queue | App-generated | On-device | No | Yes |
| Deck Metadata | Deck type (standard / sight words), titles | User | On-device + iCloud | Apple iCloud only | Yes |
| Bundled Content | Starter decks and cards packaged with the app | App bundle | On-device | No | No |
| Text-to-Speech | Spoken pronunciation playback | System | Not stored | No | No |
| Feedback Message | Feedback text entered in-app | User | Google Sheets | Yes | No |
| Feedback Email | Optional contact email (if provided) | User | Google Sheets | Yes | User-provided |
| Device Metadata | iOS version, device model, locale | System | Google Sheets | Yes | No |
| App Metadata | App version, build number | App | Google Sheets | Yes | No |

---

## Data Flow Summary

### On-device only
- Study session state (progress, queue, shuffle order)
- Text-to-speech playback (AVSpeechSynthesizer)
- Bundled starter decks (read-only JSON content in app bundle)

### Apple services
- iCloud sync for user-created decks, cards, deck metadata (including deck type)
- Data is associated with the user’s Apple ID via iCloud
- Developer does not access Apple ID or iCloud contents

### External third-party services
- **Google Apps Script Web App + Google Sheets**
  - Used only for optional in-app feedback submissions
  - Anonymous submissions allowed (unless user voluntarily provides email)
  - Basic abuse protection via shared secret token in the JSON payload

---

## Explicit Non-Collection Statements
The app does **not** collect:
- Advertising identifiers (IDFA)
- Analytics events (no analytics SDKs)
- Tracking across apps or websites
- Location data
- Contacts
- Photos/media library
- Microphone input or recordings
- Speech recordings or speech recognition data

---

## User Control & Optionality
- Creating decks and cards is user-initiated.
- Feedback submission is optional.
- Feedback email field is optional.
- No in-app login or separate accounts (relies on iCloud identity for sync).
- App functions without submitting feedback.

---

## App Store Privacy Classification Implications (Working Draft)
- Tracking: **No**
- Data linked to user: **Yes (iCloud content only)**
- Contact info: **Optional (feedback email only)**
- User content: **Yes (decks/cards created by user)**
- Diagnostics: **No (no crash/analytics SDKs)**
- Third-party data sharing: **Feedback only (Google Sheets)**

---

## Verification Checklist
- [ ] Confirm iCloud sync is enabled and used for user decks/cards (SwiftData + iCloud)
- [ ] Confirm no additional network calls exist beyond feedback submission
- [ ] Confirm no analytics/ads SDKs are present
- [ ] Confirm feedback fields written to Google Sheet match the table above
- [ ] Confirm TTS is on-device only and no audio is stored or uploaded

---

## Notes / Edge Cases
- Text-to-speech uses system APIs only; no audio is stored or transmitted.
- Feedback endpoint uses a shared secret token for abuse prevention but does not authenticate users.
- iCloud sync is Apple-managed; developer does not access user Apple IDs or iCloud contents.
