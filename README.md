# Vamo MVP

Vamo is a mobile-first travel companion app. It is not only an Austria itinerary app.

The Austria trip is the first real use case because the traveller already has a real Austria itinerary and wants to use Vamo during the actual trip. The current Austria itinerary should be treated as the first live itinerary, not as throwaway sample data.

The MVP goal is simple: help a traveller use an existing itinerary during a real holiday, make practical changes when real life interrupts the plan, and avoid missing important experiences.

Vamo is not an AI-first product yet. It is first a reliable trip guide.

## Product Direction

Vamo should feel like a travel operating system for the day.

The traveller should be able to:

- Open the app and immediately know what to do now.
- See what is coming up next.
- Check the full trip itinerary when needed.
- Adjust the plan when weather, wake-up time, restaurant hours, fatigue, or transport changes affect the day.
- Decide what to skip, move, replace, or catch up later.
- Keep track of important missed activities so they are not lost.
- Save changes locally and export backups.

## First Real Use Case

The first real use case is:

```text
Austria trip itinerary
```

This itinerary is the real trip plan that should be loaded into Vamo and used during the holiday.

The app should still be designed as a general travel companion that can support future trips later.

The product should not hard-code itself around Austria permanently. Austria is the real pilot trip.

## Primary User

The primary user is a traveller going on a planned holiday with an existing itinerary.

For the first MVP, the traveller is going to Austria and wants Vamo to help during the trip.

The user wants to:

- Use the itinerary as a practical guide.
- Prioritize important landmarks and mainstream must-see places.
- Skip lower-value or repetitive activities when time or energy is limited.
- Move missed activities to another suitable day if possible.
- Avoid losing important activities because of one bad day.
- Keep a record of completed, skipped, moved, replaced, and missed items.

## MVP Scope

The MVP should focus on personal trip usage only.

### Included In MVP

- Load one real trip itinerary into the app
- Use the Austria itinerary as the first real trip
- Home dashboard for the current day
- Current activity and next activity
- Full trip planner
- Activity detail view
- Activity editing
- Add activity
- Move activity
- Replace activity
- Mark activity as done
- Skip activity
- Missed/catch-up list
- Must-see and optional priority labels
- Local suggestions from existing itinerary data
- LocalStorage saving
- Version history and restore
- PDF export for easy viewing
- Excel-compatible export for easy editing
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
| Planner | Full trip itinerary, day selector, activity detail, catch-up planning |
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
- User preference changes during the trip

## Decision Logic

Vamo should help the user decide what to do using simple rules:

1. Protect must-see items first.
2. Move important missed items into a catch-up list.
3. Skip optional or repetitive activities first.
4. Replace closed food stops with nearby food options.
5. Prefer indoor alternatives during bad weather.
6. Use buffer or flexible days to recover missed high-value activities.
7. Keep final days lighter and more flexible.

## Target Itinerary Data Format

The current itinerary data format is useful but limited because it groups activities into broad morning, afternoon, and evening arrays.

For Vamo to become a proper travel companion, the itinerary should be transformed into a timeline-based structure.

### Minimum Required Trip Data

| Field | Required | Purpose |
|---|---:|---|
| `tripId` | Yes | Unique trip identifier |
| `tripName` | Yes | Name shown in the app |
| `destination` | Yes | Main destination or country |
| `startDate` | Recommended | Lets app map real date to trip day |
| `endDate` | Recommended | Helps calculate trip progress |
| `timezone` | Recommended | Makes current activity logic accurate |
| `days` | Yes | List of trip days |

### Minimum Required Day Data

| Field | Required | Purpose |
|---|---:|---|
| `dayNumber` | Yes | Day order |
| `date` | Recommended | Real calendar date |
| `city` | Yes | Main city or base location |
| `title` | Recommended | Short day title |
| `summary` | Recommended | What the day is about |
| `items` | Yes | Timeline activities |
| `foodIdeas` | Optional | Food/cafe options for the day |
| `transportNotes` | Optional | Route and travel notes |
| `dayNotes` | Optional | General reminders |

### Required Activity Data

| Field | Required | Purpose |
|---|---:|---|
| `itemId` | Yes | Unique activity ID |
| `startTime` | Recommended | Start time for now/next logic |
| `endTime` | Recommended | Duration and schedule logic |
| `title` | Yes | Activity name |
| `category` | Yes | Attraction, food, transport, rest, shopping, etc. |
| `priority` | Yes | Must-see, good-to-have, optional, discardable |
| `status` | Yes | Planned, done, skipped, missed, moved, replaced |
| `locationName` | Recommended | Display location |
| `address` | Optional | More precise location |
| `transportFromPrevious` | Optional | How to get there |
| `travelTimeMinutes` | Optional | Helps timing decisions |
| `bookingRequired` | Optional | Reminds user to check bookings |
| `openingHours` | Optional | Helps avoid closed places |
| `weatherSensitivity` | Optional | Indoor, outdoor, mixed |
| `catchUpEligible` | Recommended | Whether skipped item should appear in catch-up list |
| `canSkip` | Recommended | Whether item can be safely skipped |
| `notes` | Optional | Practical reminder |

### Recommended JSON Shape

```json
{
  "tripId": "austria-2026",
  "tripName": "Austria Trip",
  "destination": "Austria",
  "startDate": "2026-06-01",
  "endDate": "2026-06-13",
  "timezone": "Europe/Vienna",
  "days": [
    {
      "dayNumber": 1,
      "date": "2026-06-01",
      "city": "Vienna",
      "title": "Arrival and first Vienna walk",
      "summary": "Arrive, settle in, and keep the day light.",
      "items": [
        {
          "itemId": "day-1-arrival-vienna",
          "startTime": "14:00",
          "endTime": "15:30",
          "title": "Arrive in Vienna",
          "category": "transport",
          "priority": "must_see",
          "status": "planned",
          "locationName": "Vienna",
          "address": "",
          "transportFromPrevious": "Airport or station transfer",
          "travelTimeMinutes": 45,
          "bookingRequired": false,
          "openingHours": "",
          "weatherSensitivity": "indoor",
          "catchUpEligible": false,
          "canSkip": false,
          "notes": "Check hotel check-in time."
        }
      ],
      "foodIdeas": [],
      "transportNotes": [],
      "dayNotes": []
    }
  ]
}
```

## Data Transformation Request

To make the app more useful, the Austria itinerary should be transformed from broad day sections into the timeline item format above.

The user can provide the transformed data as:

- JSON file
- Excel file with one row per activity
- CSV file with one row per activity

The best format for the app is JSON.

The best format for manual editing is Excel.

## Local Development Commands

After editing on GitHub, run:

```powershell
cd C:\Users\jyap1\Ai-Learning-Lab
git pull origin main
cd C:\Users\jyap1\Ai-Learning-Lab\apps\holiday-companion-v1
pnpm check
pnpm build
pnpm dev
```

