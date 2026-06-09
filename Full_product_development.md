# Vamo Full Product Development Plan

## 1. Product Vision

Vamo should become a mobile-first travel companion that helps a traveller use, adapt, and preserve an itinerary during a real trip.

The product should start as a personal Austria trip guide, then grow into an intelligent itinerary assistant, and later become a shareable travel planning product.

The key product belief:

> Travel plans break. A good travel app should not only show the plan. It should help the user decide what to do when the plan changes.

## 2. Development Principles

1. Build for real trip usage first.
2. Keep the Home screen simple and immediate.
3. Put advanced tools in Planner or Profile.
4. Protect must-see activities.
5. Track skipped/missed activities instead of losing them.
6. Make every edit reversible.
7. Make light/dark mode consistent from shared tokens.
8. Keep localStorage until backend is truly needed.
9. Avoid AI complexity until itinerary state is structured and reliable.
10. Test every build on mobile.

## 3. Product Layers

| Layer | Purpose |
|---|---|
| Trip Guide Layer | Today dashboard, now/next, timeline, activity detail |
| Planning Layer | Full 13-day itinerary, move/add/edit/replace, catch-up list |
| Decision Layer | Priority, category, weather sensitivity, can-skip/catch-up rules |
| Recovery Layer | localStorage, version history, PDF/XLS/JSON exports |
| Assistant Layer | Prompt chips now, real chat later |
| Sharing Layer | Visual preview now, real share links later |
| Intelligence Layer | Internal itinerary retrieval, RAG, live data later |

## 4. Build Track A — User-Ready MVP

This is the immediate product direction.

### A1. Stabilize Theme System

Goal: Dark/light mode must apply across the entire app.

Build:

- Central theme tokens
- Shared card/button/input classes or components
- Audit all hard-coded text/background colors
- Make all popups readable in both modes

Acceptance criteria:

- No white text on white cards
- No blue text on pale blue cards unless contrast is readable
- No invisible disabled text
- Activity detail, proposed change, compare, add, move, edit, planner, profile all follow theme

### A2. Build Catch-Up System

Goal: Avoid losing important activities when plans change.

Build:

- Activity status: planned, done, skipped, missed, moved, replaced
- Priority: must-see, good-to-have, optional, discardable
- Catch-up eligibility flag
- Catch-up list inside Planner
- Move catch-up item to another day
- Mark as intentionally discarded

Acceptance criteria:

- Skipping a must-see asks whether to catch up later
- Planner shows missed/catch-up items
- User can move catch-up item to another day
- User can discard item with reason

### A3. Improve Planner For Full 13-Day Use

Goal: Planner becomes the full trip control center.

Build:

- Full 13-day day selector
- Search by city/activity/food/note
- Day route preview
- Daily timeline
- Activity spotlight
- Catch-up list
- Day summary stats

Acceptance criteria:

- User can review any day in under two taps
- User can search the full trip
- User can see important missed items
- User can add/move/edit activities from Planner

### A4. Add Priority And Category Tags

Goal: Make skip/move decisions easier.

Build:

- Activity priority field
- Activity category field
- UI chips for must-see, optional, food, transport, palace, museum, outdoor, indoor
- Simple rule prompts:
  - protect must-see
  - skip optional first
  - move weather-sensitive outdoor items if weather is bad
  - discard repeated lower-value categories if user is saturated

Acceptance criteria:

- Every activity has visible priority/category
- User can edit priority/category manually
- Skip flow behaves differently for must-see vs optional

### A5. Add Weather And Opening-Hour Awareness Without APIs

Goal: Support real trip decisions before live integrations.

Build manual fields:

- Indoor/outdoor/mixed
- Weather-sensitive yes/no
- Opening-hours check needed yes/no
- Booking required yes/no
- Live verification note

Acceptance criteria:

- Activity detail tells user what must be verified live
- Weather-sensitive activities can be moved manually
- Food stops can be replaced if closed

### A6. Strengthen Export And Recovery

Goal: Make user confident before and during trip.

Build:

- PDF itinerary backup
- Excel-compatible itinerary backup
- JSON app recovery backup
- Import JSON recovery later
- Clear reset warning

Acceptance criteria:

- User can download all three formats
- PDF is readable
- Excel is editable
- JSON can be used later for re-import

## 5. Build Track B — Assistant And Data Intelligence

This should happen after the MVP is stable.

### B1. Real Chat Input

Goal: User can type questions naturally.

Build:

- Text input
- Message history
- Suggested prompt chips
- Clear assistant responses

Acceptance criteria:

- User can ask “What should I do now?”
- User can ask “What can I skip?”
- User can ask “What did I miss?”

### B2. Itinerary-Aware Assistant

Goal: Vamo answers from internal itinerary state.

Build:

- Query current day
- Query current activity
- Query missed/catch-up list
- Query food options
- Query transport notes
- Query must-see items

Acceptance criteria:

- Assistant answers with itinerary-specific details
- Assistant does not invent unknown live data
- Assistant says when something must be verified live

### B3. Bot-Assisted Editing

Goal: User can ask for a change and review a proposed edit.

Build:

- Detect edit intent
- Create proposed change
- Accept/revise/reject flow
- Show before/after
- Save version if accepted

Acceptance criteria:

- “Make today lighter” creates a safe proposal
- “Move this to tomorrow” creates a proposal
- “Skip this palace” checks priority first

### B4. External RAG Suggestions

Goal: Suggest cafes, attractions, and alternatives from external sources later.

Build later:

- External data source strategy
- Reliability/citation layer
- Safety rules
- Cost controls
- User confirmation before adding anything

Acceptance criteria:

- External suggestions are clearly marked
- User can accept/reject
- App never silently changes itinerary

## 6. Build Track C — Sharing And Backend

This should happen when the app is useful enough for others.

### C1. Share Preview

Goal: Visual share screen exists before backend.

Build:

- Read-only preview UI
- Share scope cards
- Mock public link
- Copy button

Acceptance criteria:

- User sees what sharing will look like
- Feature is clearly labelled preview/coming soon

### C2. Backend Save Boundary

Goal: Prepare for database without rewriting app.

Build:

- Backend-ready trip payload
- Save/load adapter interface
- LocalStorage adapter remains default
- Future remote adapter stub

Acceptance criteria:

- App logic does not depend directly on localStorage everywhere
- Backend can be added later through adapter

### C3. Real Share Links

Goal: User can share trip with others.

Build:

- Read-only link
- Private trip ID
- Basic share settings
- Optional expiry

Acceptance criteria:

- Shared user can view itinerary but not edit
- Owner can revoke or regenerate link later

### C4. Accounts And Multi-Device

Goal: Save trips across devices.

Build later:

- Login
- Saved trips
- Trip ownership
- Cloud version history

Acceptance criteria:

- User can open same trip on phone/laptop
- Data persists beyond browser localStorage

## 7. Build Track D — Trip Creation And Import

This is future product expansion.

### D1. Import Existing Itinerary

Goal: User can import plans from outside Vamo.

Build:

- Paste itinerary text
- Upload JSON
- Upload Excel
- Upload PDF later
- Convert to structured timeline

Acceptance criteria:

- User can import a trip without manually entering every activity
- Imported data can be reviewed before saving

### D2. Guided Trip Creator

Goal: User can create new trips from preferences.

Build:

- Destination
- Dates
- Pace
- Interests
- Must-see list
- Food preferences
- Budget roughness

Acceptance criteria:

- User can generate a draft itinerary
- User can edit before saving

### D3. AI Trip Generation

Goal: AI helps create and optimize itineraries.

Build later:

- Prompt templates
- User preference model
- External research/RAG
- Guardrails
- Cost limits

Acceptance criteria:

- Generated plan is structured
- User approves before saving
- Sources and uncertainty are clear

## 8. Build Track E — Mobile App Readiness

### E1. PWA Install

Goal: App can be installed to home screen.

Build:

- Manifest
- App icons
- Theme color
- Offline shell

Acceptance criteria:

- User can install on phone
- App opens like a mobile app

### E2. Offline Mode

Goal: Itinerary stays usable with poor internet.

Build:

- Cache app shell
- Keep local trip available
- Show offline indicator

Acceptance criteria:

- Current trip can be viewed offline
- Edits save locally and sync later when backend exists

### E3. React Native / Hybrid Path

Goal: Keep future mobile app migration possible.

Principles:

- Keep state logic separate from UI
- Keep business rules in shared helpers
- Avoid browser-only APIs deep in core logic
- Keep components mobile-oriented

## 9. Recommended Build Order From Now

| Order | Build item | Why it matters |
|---:|---|---|
| 1 | Theme utility cleanup | Prevent repeated light/dark mode breakages |
| 2 | Catch-up system | Directly solves the user’s core travel problem |
| 3 | Priority/category tags | Helps user decide what to skip or protect |
| 4 | Planner catch-up view | Shows missed important items and recovery options |
| 5 | Weather/opening-hour manual flags | Supports real trip decision-making without APIs |
| 6 | State manager cleanup | Keeps code maintainable before more features |
| 7 | Structured timeline model | Enables better assistant, import, sharing, and mobile app future |
| 8 | Itinerary-aware assistant | Makes Vamo smarter without external RAG first |
| 9 | PWA install | Makes the app feel more native for travel use |
| 10 | Backend/share links | Only after personal MVP is solid |

## 10. Future Parking Lot

These are good ideas but should not distract from the personal-trip MVP:

- Real weather API
- Google Maps route integration
- Restaurant opening-hour lookup
- External attraction recommendations
- Full RAG pipeline
- Public sharing marketplace
- Collaborative trip planning
- Expense tracking
- Travel journal/photo diary
- Booking integrations
- Native iOS/Android app
- Monetization

## 11. Product Readiness Checklist

The product is user-ready for the Austria trip when:

- Home shows now/next clearly
- Planner shows all 13 days clearly
- Activity detail is readable in dark and light mode
- User can edit/add/move/skip/replace activities
- User can mark done
- User can catch up missed important items
- User can export PDF/XLS/JSON backups
- Version history works
- Reset works
- Mobile phone testing feels comfortable
- No important text is camouflaged in light mode
- App runs locally and can be opened on phone through Vite network URL
