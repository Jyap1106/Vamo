# Vamo Full Product Development Plan

## 1. Product Vision

Vamo should become a mobile-first travel companion that helps a traveller use, adapt, and preserve an itinerary during a real trip.

The product starts with the user’s real Austria itinerary because that is the immediate live use case. Austria is not the product limit. Austria is the first itinerary used to validate the product.

The key product belief:

> Travel plans break. A good travel app should not only show the plan. It should help the user decide what to do when the plan changes.

## 2. Product Narrative

Vamo is not just a 13-day Austria itinerary app.

Vamo is a general travel companion app for existing itineraries.

The first loaded trip is the real Austria itinerary because:

- The user already has the trip planned.
- The trip will be used in real life.
- The product can be tested against real travel decisions.
- The itinerary contains multiple cities, landmarks, food ideas, transport notes, and flexible decision points.

The product should be built so another itinerary can be imported later using the same data format.

## 3. Development Principles

1. Build for real trip usage first.
2. Treat Austria as the first live itinerary, not throwaway sample data.
3. Keep the Home screen simple and immediate.
4. Put advanced tools in Planner or Profile.
5. Protect must-see activities.
6. Track skipped/missed activities instead of losing them.
7. Make every edit reversible.
8. Make light/dark mode consistent from shared tokens.
9. Keep localStorage until backend is truly needed.
10. Avoid AI complexity until itinerary state is structured and reliable.
11. Use a reusable trip data format for future trips.
12. Test every build on mobile.

## 4. Product Layers

| Layer | Purpose |
|---|---|
| Trip Guide Layer | Today dashboard, now/next, timeline, activity detail |
| Planning Layer | Full itinerary, move/add/edit/replace, catch-up list |
| Decision Layer | Priority, category, weather sensitivity, can-skip/catch-up rules |
| Recovery Layer | localStorage, version history, PDF/XLS/JSON exports |
| Data Layer | Reusable trip schema for Austria and future trips |
| Assistant Layer | Prompt chips now, real chat later |
| Sharing Layer | Visual preview now, real share links later |
| Intelligence Layer | Internal itinerary retrieval, RAG, live data later |

## 5. Build Track A — User-Ready MVP

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

### A2. Define The Reusable Trip Data Format

Goal: Move Vamo away from Austria-only assumptions and toward a reusable travel itinerary structure.

Build:

- Trip schema
- Day schema
- Activity item schema
- Priority values
- Status values
- Weather sensitivity values
- Catch-up eligibility
- Source/original text field

Acceptance criteria:

- Austria itinerary can be represented as real trip data
- Future trips can use the same format
- App does not depend on hard-coded morning/afternoon/evening arrays forever
- Data can be edited externally in Excel and imported later

### A3. Transform Austria Itinerary Into Timeline Data

Goal: Convert the current Austria itinerary into the target format.

Build:

- One activity per row/item
- Real or estimated start/end times
- Priority labels
- Category labels
- Location fields
- Transport fields
- Notes fields
- Catch-up eligibility
- Can-skip guidance

Acceptance criteria:

- Every meaningful itinerary item becomes a timeline item
- Must-see landmarks are clearly marked
- Optional/repetitive activities are marked lower priority
- Food/cafe options are distinguishable from attractions
- Activities can be moved/skipped/caught up reliably

### A4. Build Catch-Up System

Goal: Avoid losing important activities when plans change.

Build:

- Activity status: planned, done, skipped, missed, moved, replaced, discarded
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

### A5. Improve Planner For Full Trip Use

Goal: Planner becomes the full trip control center.

Build:

- Full day selector
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

### A6. Improve Activity Detail

Goal: Activity detail becomes the main decision screen.

Build:

- Priority label
- Status label
- Time and duration
- Location and transport
- Weather/opening-hour reminder
- Can-skip guidance
- Catch-up action
- Replace/move/edit/done actions

Acceptance criteria:

- User can decide whether to do, skip, move, or replace an item from one screen
- Must-see items are visually clear
- Optional items feel safe to skip

### A7. Local Suggestions

Goal: Give useful alternatives from the existing itinerary data without external RAG.

Build:

- Food suggestion cards
- Lighter day suggestion
- Nearby/flexible stop suggestion
- Indoor/outdoor suggestion based on item tags
- Repetitive-activity warning

Acceptance criteria:

- Suggestions come from current trip data
- No external API required
- Suggestions are actionable

### A8. Recovery And Export

Goal: User can preserve and recover trip data.

Build:

- PDF export for viewing
- Excel-compatible export for editing
- JSON export for recovery
- Local reset
- Version restore

Acceptance criteria:

- User can export the itinerary before leaving
- User can export after edits
- User can restore a previous version
- User can reset if local data breaks

## 6. Build Track B — Better Data And State Architecture

This track makes the app easier to maintain.

### B1. Proper Timeline Data Model

Current data model:

```text
morning[]
afternoon[]
evening[]
```

Target data model:

```text
items[]
```

Each item should contain:

- ID
- day number
- start time
- end time
- title
- category
- priority
- status
- location
- transport
- opening/check notes
- catch-up flags

### B2. State Manager Cleanup

Goal: Move large itinerary logic out of `Home.tsx`.

Build files such as:

```text
lib/itineraryStateManager.ts
lib/itineraryTransform.ts
lib/activityDecisionRules.ts
lib/catchUpManager.ts
```

Acceptance criteria:

- `Home.tsx` becomes mostly orchestration
- Itinerary logic is reusable
- Future backend integration is easier

### B3. Data Import Preparation

Goal: Prepare for future import without building full import yet.

Build:

- JSON validator
- Spreadsheet column mapping plan
- Import preview screen later
- Error messages for missing required fields

Acceptance criteria:

- User knows exactly what data format to provide
- App can reject malformed data safely later

## 7. Build Track C — Assistant And Intelligence

This is future work after the itinerary state is reliable.

### C1. Itinerary-Aware Assistant

Goal: Assistant can answer questions from itinerary data.

Examples:

- “What should I do now?”
- “What can I skip?”
- “What did I miss in Vienna?”
- “What food options do I have today?”
- “Can I move this palace to another day?”

### C2. Real Chat Input

Goal: Move beyond prompt chips.

Build:

- Text input
- Message history
- Action buttons in assistant responses
- Edit proposal flow

### C3. External RAG Suggestions

Goal: Use external data later for restaurants, weather, attractions, opening hours, and route suggestions.

Not needed for MVP.

## 8. Build Track D — Sharing And Multi-Trip Product

This track makes Vamo useful beyond personal use.

### D1. Share Itinerary

Goal: Create read-only itinerary sharing.

Build:

- Share preview screen
- Read-only mode
- Copy link
- Share one day
- Share full trip

Requires backend later.

### D2. Multiple Trips

Goal: Support more than Austria.

Build:

- Trip list
- Create/import trip
- Switch active trip
- Archive trips

### D3. Backend Saving

Goal: Save trips outside local browser.

Possible future options:

- Supabase
- Firebase
- Postgres backend
- Hosted JSON API

Not needed for personal MVP.

## 9. Build Track E — Post-Trip Features

Post-trip is not urgent for the first MVP but should be considered.

Potential features:

- Trip completion summary
- Completed vs skipped activities
- Photo/memory notes
- Export final itinerary
- Save “places I loved”
- Reuse trip as template
- Share final trip summary

## 10. Target Data Format

### 10.1 JSON Trip Format

```json
{
  "tripId": "austria-2026",
  "tripName": "Austria Trip",
  "destination": "Austria",
  "startDate": "2026-06-01",
  "endDate": "2026-06-13",
  "timezone": "Europe/Vienna",
  "currency": "EUR",
  "travellerStyle": ["culture", "food", "scenic", "relaxed"],
  "days": [
    {
      "dayId": "day-1",
      "dayNumber": 1,
      "date": "2026-06-01",
      "city": "Vienna",
      "title": "Arrival in Vienna",
      "summary": "Arrive, settle in, and keep the day light.",
      "overnightLocation": "Vienna",
      "bufferLevel": "medium",
      "items": [
        {
          "itemId": "day-1-arrival-vienna",
          "dayNumber": 1,
          "startTime": "14:00",
          "endTime": "15:30",
          "title": "Arrive in Vienna",
          "category": "transport",
          "priority": "must_see",
          "status": "planned",
          "locationName": "Vienna",
          "address": "",
          "area": "Vienna",
          "googleMapsUrl": "",
          "transportFromPrevious": "Airport or station transfer",
          "travelTimeMinutes": 45,
          "bookingRequired": false,
          "bookingReference": "",
          "openingHours": "",
          "reservationTime": "",
          "costEstimate": "",
          "weatherSensitivity": "indoor",
          "physicalIntensity": "low",
          "similarityGroup": "arrival",
          "catchUpEligible": false,
          "canSkip": false,
          "replacementTags": ["rest", "light"],
          "notes": "Check hotel check-in time.",
          "sourceText": "Original itinerary text goes here"
        }
      ],
      "foodIdeas": [],
      "transportNotes": [],
      "dayNotes": []
    }
  ]
}
```

### 10.2 Spreadsheet Format

One row per activity.

| Column | Required | Example |
|---|---:|---|
| Trip ID | Yes | austria-2026 |
| Trip Name | Yes | Austria Trip |
| Destination | Yes | Austria |
| Start Date | Recommended | 2026-06-01 |
| End Date | Recommended | 2026-06-13 |
| Timezone | Recommended | Europe/Vienna |
| Day Number | Yes | 2 |
| Date | Recommended | 2026-06-02 |
| City | Yes | Vienna |
| Day Title | Recommended | Vienna palaces and landmarks |
| Day Summary | Recommended | Main Vienna sightseeing day |
| Start Time | Recommended | 09:00 |
| End Time | Recommended | 10:30 |
| Activity Title | Yes | Schönbrunn Palace |
| Category | Yes | attraction |
| Priority | Yes | must_see |
| Status | Yes | planned |
| Location Name | Recommended | Schönbrunn Palace |
| Address | Optional | Vienna, Austria |
| Area | Optional | Vienna |
| Transport From Previous | Optional | U-Bahn / tram |
| Travel Time Minutes | Optional | 25 |
| Booking Required | Optional | TRUE |
| Booking Reference | Optional | Ticket ID |
| Opening Hours | Optional | Check live |
| Reservation Time | Optional | 19:00 |
| Cost Estimate | Optional | Medium |
| Weather Sensitivity | Optional | mixed |
| Physical Intensity | Optional | medium |
| Similarity Group | Optional | palace |
| Catch Up Eligible | Recommended | TRUE |
| Can Skip | Recommended | FALSE |
| Replacement Tags | Optional | indoor, nearby, light |
| Notes | Optional | Verify ticket availability live |
| Source Text | Optional | Original itinerary line |

## 11. Suggested Build Order From Here

| Priority | Module | Why |
|---:|---|---|
| 1 | Data format transformation | The app needs proper activity items before it can make good decisions |
| 2 | Catch-up system | This directly solves the user’s concern about not missing important items |
| 3 | Planner catch-up view | User needs to see what was missed and where to recover it |
| 4 | Activity priority editing | User needs to label must-see vs optional |
| 5 | State manager cleanup | Keeps future development manageable |
| 6 | Itinerary-aware assistant | Useful once data is structured |
| 7 | Real import flow | Lets future trips be added |
| 8 | Backend and sharing | Needed after personal MVP proves useful |

## 12. Future Good-To-Have Features

These are valuable but not needed for the immediate user-ready MVP:

- Live weather API
- Restaurant opening-hour lookup
- Maps and route integration
- AI-generated itinerary suggestions
- External RAG attraction recommendations
- Multi-user sharing
- Login and cloud save
- Native mobile app
- Photo journal
- Trip memories and post-trip recap
- Collaborative planning
- Drag-and-drop itinerary reorder

## 13. Product Manager Recommendation

The next product step is not more UI polish.

The next product step should be:

```text
Transform the real Austria itinerary into Vamo’s timeline activity data format.
```

Reason:

- The current grouped format limits the product.
- Catch-up logic needs per-activity priority/status fields.
- The assistant will eventually need structured itinerary context.
- Future trips need a reusable data contract.

The app should remain visually mobile-first, but the next major unlock is data quality.

