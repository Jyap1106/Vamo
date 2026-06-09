# Vamo Product Requirements Document

## 1. Product Summary

Vamo is a mobile-first travel companion app for travellers who already have an itinerary and need help using it during the actual trip.

The Austria itinerary is the first real use case. It is not just a sample itinerary. It is the user’s real itinerary and should be treated as the first live itinerary loaded into the product.

The long-term product should support any trip. The MVP uses Austria because that is the immediate real-world trip.

The MVP should not try to become a full travel marketplace, AI trip generator, or social sharing platform. Those can come later. The immediate product goal is to make an existing itinerary usable in real life.

## 2. Product Objective

Create a user-ready travel companion that helps the user:

- Follow the itinerary day by day.
- Know what to do now and what is coming next.
- Make itinerary changes quickly during the trip.
- Decide what to skip, move, replace, or catch up later.
- Preserve important activities if they are skipped.
- Export backups for viewing and editing.
- Use the app comfortably on mobile.

## 3. Product Positioning

Vamo should be positioned as:

```text
A travel companion for using and adapting an itinerary during a real trip.
```

It should not be positioned as:

```text
An Austria-only itinerary viewer.
```

Austria is the first live itinerary. The product should be designed so another trip can be loaded later with the same structure.

## 4. Product Lenses

### 4.1 Product Manager Lens

The MVP must solve one strong use case before expanding:

> “I am on holiday now. Tell me what my plan is, help me adjust when life changes, and make sure I do not miss the important things.”

The product should optimize for:

- Speed of understanding
- Low-friction decisions
- Trust in saved changes
- Mobile readability
- Recovery from missed plans
- Offline/local resilience
- Reusability for future trips

The product should avoid:

- Hard-coding itself permanently around Austria
- Too many future features on the main screen
- AI complexity before the itinerary system is reliable
- Heavy backend work before personal-trip usability is proven
- Overbuilding planning tools that are not needed during the trip

### 4.2 Holiday Planner Lens

Before and during a holiday, a traveller needs more than a list of activities.

The planner needs to know:

- Which activities are must-see
- Which activities are optional
- Which activities can move to another day
- Which activities are weather-sensitive
- Which activities require booking or opening-hour checks
- Which activities are repetitive and can be sacrificed
- Which days have buffer time
- Which cities will be revisited later in the trip
- Which missed activities should be caught before leaving the area

A good trip guide must help the traveller make trade-offs.

Example trade-off:

```text
If I wake up late on a Vienna palace day, should I still see both Schönbrunn and Belvedere?
```

Vamo should help by showing:

- Priority
- Category
- Time required
- Whether it can be caught later
- Whether a similar activity already happened
- Whether weather or opening hours matter

### 4.3 Traveller/User Lens

The user’s thought process during the trip:

- “What am I supposed to do now?”
- “What is next?”
- “Am I late?”
- “Can I skip this?”
- “Will I regret skipping this?”
- “Can I move this to another day?”
- “Is this place open?”
- “Is the weather suitable?”
- “I have seen too many palaces. Can I replace this with food or a walk?”
- “I may not return to Vienna. What must I absolutely not miss?”

The product should answer these questions quickly without forcing the user into complex editing screens.

## 5. MVP Definition

The MVP is complete when the user can use Vamo as a practical guide for the full Austria trip and the app remains reusable for future trips.

### 5.1 MVP Must-Have Features

| Feature | Requirement |
|---|---|
| Trip loading | Load one real itinerary into the app, starting with the Austria itinerary |
| Today dashboard | Shows current day, city, current activity, next activity, progress, quick actions |
| Full itinerary overview | Shows all trip days with activities, food, transport, and notes |
| Activity detail | Shows time, location, transport, remarks, priority, status, and actions |
| Activity editing | User can edit title, time, location, transport, and notes |
| Add activity | User can add a new stop, food break, transport note, or free-time block |
| Move activity | User can move an activity to another time block or another day |
| Replace activity | User can replace an activity with food, lighter activity, nearby option, or free time |
| Skip activity | User can skip an item and decide whether it should be caught up later |
| Mark done | User can mark an item as completed |
| Catch-up list | Important skipped/missed activities are stored for possible recovery later |
| Priority labels | Activities can be marked must-see, good-to-have, optional, or discardable |
| Local suggestions | Suggestions come from existing itinerary data, food options, notes, and activity categories |
| Local saving | Changes persist with localStorage |
| Version history | Confirmed changes create restorable versions |
| Backup export | User can download PDF, Excel-compatible XLS, and JSON backup |
| Theme support | Dark and light modes must be readable across all cards and popups |

### 5.2 MVP Should-Have Features

| Feature | Requirement |
|---|---|
| Search full itinerary | User can search city, activity, food, or notes |
| Day stats | Show activity count, estimated duration, edited status |
| Basic decision hints | Show “safe to skip,” “must-see,” or “catch up later” indicators |
| Import placeholder | Show future upload/create trip entry point in Profile |
| Share preview | Show visual share preview, but real share links can come later |

### 5.3 Not Required For MVP

| Feature | Reason to defer |
|---|---|
| Real AI chatbot | Itinerary state must become reliable first |
| External RAG | Not needed for personal trip MVP |
| Live weather API | Can use manual weather checks first |
| Live restaurant opening hours | Can be noted as “verify live” first |
| Maps API | Useful later, not required for first real trip use |
| Backend database | localStorage is acceptable for personal MVP |
| Login system | Not needed until multi-user or multi-device use |
| Real share links | Future phase |
| Native app | Mobile web first |

## 6. Target User Flows

### 6.1 Start Of Day Flow

```text
Open Vamo
↓
See current day and city
↓
See current activity and next activity
↓
Check timeline
↓
Follow plan
```

### 6.2 Running Late Flow

```text
Open Vamo
↓
See that current activity is delayed
↓
Choose “make today lighter” or tap an activity
↓
Skip, replace, or move item
↓
If important, add to catch-up list
↓
Save new version
```

### 6.3 Closed Restaurant Flow

```text
Tap food activity
↓
Choose replace
↓
Pick another food/cafe option from local itinerary data
↓
Confirm change
↓
Save locally
```

### 6.4 Must-See Protection Flow

```text
Try to skip a must-see item
↓
Vamo asks whether to catch it later
↓
User chooses catch up later or discard
↓
Planner updates catch-up list
```

### 6.5 Post-Trip Flow

```text
Open Profile
↓
Export PDF for viewing
↓
Export Excel-compatible file for editing/archive
↓
Export JSON for app recovery
```

## 7. Itinerary Data Requirements

The current itinerary data format is useful for a first prototype but too limited for a real trip companion.

Current structure:

```text
Day
├── morning[]
├── afternoon[]
├── evening[]
├── food[]
├── transport[]
└── notes[]
```

Target structure:

```text
Trip
└── Days
    └── Timeline Items
```

Each timeline item should have enough context for editing, moving, skipping, catch-up, and assistant guidance.

## 8. Recommended Data Contract

### 8.1 Trip Level

| Field | Type | Required | Notes |
|---|---|---:|---|
| `tripId` | string | Yes | Stable ID, example `austria-2026` |
| `tripName` | string | Yes | Display name |
| `destination` | string | Yes | Country/region |
| `startDate` | string | Recommended | ISO date, example `2026-06-01` |
| `endDate` | string | Recommended | ISO date |
| `timezone` | string | Recommended | Example `Europe/Vienna` |
| `currency` | string | Optional | Example `EUR` |
| `travellerStyle` | string[] | Optional | Relaxed, food, culture, scenic |
| `days` | Day[] | Yes | Full itinerary |

### 8.2 Day Level

| Field | Type | Required | Notes |
|---|---|---:|---|
| `dayId` | string | Yes | Stable day ID |
| `dayNumber` | number | Yes | Day order |
| `date` | string | Recommended | Real trip date |
| `city` | string | Yes | Main base city |
| `title` | string | Recommended | Short day title |
| `summary` | string | Recommended | Day summary |
| `overnightLocation` | string | Optional | Useful for transport planning |
| `items` | ActivityItem[] | Yes | Timeline activities |
| `foodIdeas` | string[] | Optional | Day food options |
| `transportNotes` | string[] | Optional | Train/tram/walk notes |
| `dayNotes` | string[] | Optional | General reminders |
| `bufferLevel` | string | Optional | none, light, medium, high |

### 8.3 Activity Item Level

| Field | Type | Required | Notes |
|---|---|---:|---|
| `itemId` | string | Yes | Stable item ID |
| `dayNumber` | number | Yes | Parent day |
| `startTime` | string | Recommended | `HH:mm` |
| `endTime` | string | Recommended | `HH:mm` |
| `title` | string | Yes | Activity title |
| `category` | string | Yes | attraction, food, transport, rest, shopping, hotel, scenic, museum |
| `priority` | string | Yes | must_see, good_to_have, optional, discardable |
| `status` | string | Yes | planned, done, skipped, missed, moved, replaced |
| `locationName` | string | Recommended | Display name |
| `address` | string | Optional | Physical address |
| `area` | string | Optional | Neighbourhood/area |
| `googleMapsUrl` | string | Optional | Can be empty initially |
| `transportFromPrevious` | string | Optional | How to get there |
| `travelTimeMinutes` | number | Optional | Helps schedule decisions |
| `bookingRequired` | boolean | Optional | True/false |
| `bookingReference` | string | Optional | Ticket/reservation info |
| `openingHours` | string | Optional | Human-readable |
| `reservationTime` | string | Optional | For restaurants/events |
| `costEstimate` | string | Optional | Free, low, medium, high, or amount |
| `weatherSensitivity` | string | Optional | indoor, outdoor, mixed |
| `physicalIntensity` | string | Optional | low, medium, high |
| `similarityGroup` | string | Optional | palace, museum, church, viewpoint, cafe |
| `catchUpEligible` | boolean | Recommended | Should missed item be recoverable? |
| `canSkip` | boolean | Recommended | Safe to skip? |
| `replacementTags` | string[] | Optional | food, indoor, nearby, light, scenic |
| `notes` | string | Optional | Practical note |
| `sourceText` | string | Optional | Original itinerary text |

## 9. Spreadsheet Format For User Transformation

If the user wants to transform itinerary data manually, the easiest editing format is a spreadsheet with one row per activity.

Recommended columns:

| Column | Example |
|---|---|
| Trip ID | austria-2026 |
| Trip Name | Austria Trip |
| Day Number | 2 |
| Date | 2026-06-02 |
| City | Vienna |
| Day Title | Vienna palaces and classic landmarks |
| Start Time | 09:00 |
| End Time | 10:30 |
| Activity Title | Schönbrunn Palace |
| Category | attraction |
| Priority | must_see |
| Status | planned |
| Location Name | Schönbrunn Palace |
| Address | Vienna, Austria |
| Area | Vienna |
| Transport From Previous | U-Bahn / tram |
| Travel Time Minutes | 25 |
| Booking Required | TRUE |
| Opening Hours | Check live |
| Weather Sensitivity | mixed |
| Physical Intensity | medium |
| Similarity Group | palace |
| Catch Up Eligible | TRUE |
| Can Skip | FALSE |
| Replacement Tags | indoor, nearby, light |
| Notes | Verify ticket availability live |
| Source Text | Original itinerary line |

## 10. Acceptance Criteria

The MVP is user-ready when:

- The real Austria itinerary can be loaded as a trip.
- The app does not describe the Austria data as throwaway sample data.
- The data structure can support future non-Austria trips.
- The user can follow today’s plan quickly.
- The user can edit, move, replace, skip, and mark done.
- Important skipped items are not lost.
- Local changes persist.
- Backup export works.
- Dark and light modes are readable.
- The app works comfortably on mobile.

