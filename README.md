# Vamo MVP

Vamo is a personal mobile-first Austria trip companion. The MVP goal is simple: help the traveller use an existing 13-day Austria itinerary during the actual trip, make practical changes when real life interrupts the plan, and avoid missing important experiences.

This is not an AI-first product yet. It is first a reliable trip guide.

## Product Direction

Vamo should feel like a travel operating system for the day:

- Open the app and immediately know what to do now.
- See what is coming up next.
- Check the full 13-day itinerary when needed.
- Adjust the day when weather, wake-up time, restaurant hours, fatigue, or transport changes affect the plan.
- Keep track of skipped or missed activities so important experiences can be caught later.
- Save changes locally and export backups.

## Primary User

The primary user is the traveller going to Austria with an existing itinerary.

The user wants to:

- Use the itinerary as a practical guide during the trip.
- Prioritize important landmarks and mainstream must-see places.
- Skip lower-value or repetitive activities when time or energy is limited.
- Move missed activities to another suitable day if possible.
- Keep a record of completed, skipped, moved, and missed items.

## MVP Scope

The MVP should focus on personal trip usage only.

### Included In MVP

- 13-day Austria itinerary loaded from local app data
- Home dashboard for current day
- Current activity and next activity
- Full itinerary planner
- Activity detail view
- Activity editing
- Add activity
- Move activity
- Replace activity
- Mark done
- Skip activity
- Missed/catch-up list
- Must-see and optional priority labels
- Local suggestions from existing itinerary data
- LocalStorage saving
- Version history and restore
- PDF export for viewing
- Excel-compatible export for editing
- JSON export for app recovery
- Dark and light mode with consistent readable contrast

### Not Required For MVP

- Real AI chatbot
- External RAG suggestions
- Live weather API
- Live restaurant opening hours API
- Maps API
- Backend database
- Login system
- Public sharing links
- Collaborative trip editing
- Drag-and-drop reorder
- Native mobile app

## Core Navigation

The MVP should use three bottom tabs:

| Tab | Purpose |
|---|---|
| Home | Today guide: now, next, timeline, quick actions, smart local suggestions |
| Planner | Full 13-day itinerary, day selector, activity detail, catch-up planning |
| Profile | Settings, theme, backup exports, reset, future import/create placeholders |

## Main User Flow

```text
Open Vamo
↓
See current day, current activity, next activity
↓
Follow plan or inspect details
↓
If something changes, edit / skip / move / replace
↓
Important skipped items enter catch-up list
↓
Save locally and continue trip
```

## Trip Reality The App Must Support

Trips rarely follow the original plan exactly. Vamo must support practical changes caused by:

- Waking up late
- Bad weather
- Restaurant or cafe closed
- Museum or attraction opening-hour changes
- Tiredness or overpacked schedule
- Transport delays
- Too many similar experiences in a row
- Desire to prioritize major landmarks before leaving a city

## Decision Logic

Vamo should help the user decide what to do using simple rules:

1. Protect must-see items first.
2. Move important missed items into a catch-up list.
3. Skip optional or repetitive activities first.
4. Replace closed food stops with nearby food options.
5. Prefer indoor alternatives during bad weather.
6. Use buffer or flexible days to recover missed high-value activities.
7. Keep final days lighter and more flexible.

## Data Philosophy

The current sample itinerary should remain protected. The app should work from app-friendly local data and user edits should save separately through localStorage.

Activities should eventually be represented as structured timeline items, not only morning/afternoon/evening text arrays.

Each activity should support:

- Time
- Title
- Location
- Transport
- Notes
- Priority
- Category
- Status
- Weather sensitivity
- Booking/opening-hour notes
- Catch-up eligibility

## Build Philosophy

Build for trip usefulness before product complexity.

The MVP is successful if the user can confidently rely on Vamo during the Austria trip without needing backend, AI, or live integrations.

## Local Development

Use GitHub as source of truth. Pull locally and test with PowerShell.

```powershell
cd C:\Users\jyap1\Ai-Learning-Lab
git pull origin main
cd C:\Users\jyap1\Ai-Learning-Lab\apps\holiday-companion-v1
pnpm check
pnpm build
pnpm dev
```

Open the local URL shown by Vite, usually:

```text
http://localhost:3000/
```

For mobile testing, open the Vite network URL on a phone connected to the same Wi-Fi.
