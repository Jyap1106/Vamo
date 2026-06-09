# Vamo Product Requirements Document

## 1. Product Summary

Vamo is a mobile-first itinerary companion for a 13-day Austria trip. The MVP is designed for personal use during the actual holiday. It helps the traveller understand today’s plan, make decisions when the itinerary changes, and avoid missing important experiences.

The MVP should not try to become a full travel marketplace, AI trip generator, or social sharing platform. Those can come later. The immediate product goal is to make the existing itinerary usable in real life.

## 2. Product Objective

Create a user-ready travel companion that helps the user:

- Follow the itinerary day by day.
- Know what to do now and what is coming next.
- Make itinerary changes quickly during the trip.
- Preserve important activities if they are skipped.
- Export backups for viewing and editing.
- Use the app comfortably on mobile.

## 3. Product Lenses

### 3.1 Product Manager Lens

The MVP must solve one strong use case before expanding:

> “I am in Austria now. Tell me what my plan is, help me adjust when life changes, and make sure I do not miss the important things.”

The product should optimize for:

- Speed of understanding
- Low-friction decisions
- Trust in saved changes
- Mobile readability
- Recovery from missed plans
- Offline/local resilience

The product should avoid:

- Too many future features on the main screen
- AI complexity before the itinerary system is reliable
- Heavy backend work before personal-trip usability is proven
- Overbuilding planning tools that are not needed during the trip

### 3.2 Holiday Planner Lens

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

### 3.3 Traveller/User Lens

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

## 4. MVP Definition

The MVP is complete when the user can use Vamo as a practical guide for the full Austria trip.

### 4.1 MVP Must-Have Features

| Feature | Requirement |
|---|---|
| Today dashboard | Shows current day, city, current activity, next activity, progress, quick actions |
| Full itinerary overview | Shows all 13 days with activities, food, transport, and notes |
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

### 4.2 MVP Should-Have Features

| Feature | Requirement |
|---|---|
| Weather manual flag | Activity can be marked indoor/outdoor/weather-sensitive without live API |
| Opening-hour reminder | Activity can show “verify live” or “requires opening-hours check” |
| Buffer-day suggestions | App can highlight suitable days for catch-up items |
| Duplicate-category warning | App can warn when skipping another similar activity is low-risk |
| Trip completion view | User can see completed, skipped, moved, and missed items |

### 4.3 MVP Not Required

| Feature | Reason to defer |
|---|---|
| Real chatbot AI | Prompt-chip/local assistant is enough for personal MVP |
| External RAG | Useful later, but not needed before itinerary editing is reliable |
| Live weather API | Manual weather sensitivity is enough first |
| Live restaurant hours | User can verify manually first |
| Google Maps routing | Nice to have, but can be added later |
| Backend database | localStorage is enough for personal-trip MVP |
| User accounts | Not needed for single-user Austria trip |
| Sharing links | Can be preview-only now; real sharing later |
| Drag-and-drop | Manual move is enough for MVP |
| Native mobile app | Mobile web and potential PWA path are enough first |

## 5. Information Architecture

### 5.1 Home

Purpose: Today’s trip guide.

Must show:

- App name
- Country/city/weather area
- Current time
- Current day
- Current activity
- Next activity
- Progress through the day
- Quick actions: Ask Vamo, Edit Day, Share Preview
- Next-up timeline
- Local suggestions

### 5.2 Planner

Purpose: Whole trip overview and adjustment workspace.

Must show:

- 13-day selector
- Selected day route preview
- Selected day timeline
- Activity detail spotlight
- Add stop
- Full itinerary overview/search
- Catch-up list

### 5.3 Profile

Purpose: Settings and recovery.

Must show:

- Trip summary
- Theme toggle
- Backup exports
- Version history
- Reset sample trip
- Create/import placeholders
- Future sharing/settings placeholders

## 6. Core User Stories

### Story 1: Open app during the trip

As a traveller, I want to open Vamo and immediately know what I should be doing now and what is coming next.

Acceptance criteria:

- Home loads directly into today’s view.
- Current activity is visually dominant.
- Next activity is visible without digging through menus.
- Current time is shown clearly.

### Story 2: Running late

As a traveller, I want to know what I can skip or move when I am running late.

Acceptance criteria:

- User can tap an activity and choose Skip, Move, Replace, or Free Time.
- Must-see items are not silently discarded.
- Skipped important items appear in catch-up list.
- Version history records the change.

### Story 3: Restaurant closed

As a traveller, I want to replace a food stop if the restaurant or cafe is closed.

Acceptance criteria:

- User can replace activity with food/cafe option.
- Replacement suggestions can come from the day’s existing food list.
- User confirms before saving.

### Story 4: Too many similar activities

As a traveller, I want to skip a repetitive activity if I have already done many similar ones.

Acceptance criteria:

- Activities have category labels.
- User can decide to discard optional/repetitive activities.
- Must-see/high-priority activities are clearly marked.

### Story 5: Catch missed items later

As a traveller, I want to see what I missed and possibly move it to another day.

Acceptance criteria:

- Skipped/missed activities can be marked as catch-up items.
- Planner shows a catch-up list.
- User can move a catch-up item to another day.

### Story 6: Backup itinerary

As a traveller, I want a backup that I can view or edit outside the app.

Acceptance criteria:

- PDF export downloads a readable itinerary.
- Excel-compatible export downloads an editable file.
- JSON export downloads app-recovery data.

## 7. Core Data Model Direction

The current morning/afternoon/evening arrays are useful for early development but should evolve into structured timeline items.

Recommended activity fields:

| Field | Purpose |
|---|---|
| id | Stable activity ID |
| dayNumber | Which day it belongs to |
| startTime | Activity start |
| endTime | Activity end |
| title | Activity name |
| city | Base city/area |
| location | Place/address/area |
| transport | How to get there |
| notes | Tickets, reminders, context |
| category | palace, museum, food, transport, outdoor, market, viewpoint, free-time |
| priority | must-see, good-to-have, optional, discardable |
| status | planned, done, skipped, moved, replaced, missed |
| catchUpEligible | Whether it should be shown in catch-up list |
| weatherSensitive | indoor, outdoor, mixed, unknown |
| openingHoursNote | Manual note or future live-check field |
| bookingRequired | Whether tickets/reservations matter |
| originalDayNumber | Where it started before moving |
| movedToDayNumber | Where it moved, if moved |
| skipReason | Why user skipped it |

## 8. Success Metrics

For personal MVP, success is qualitative.

The app is successful if:

- User can use it during the trip without confusion.
- User can change the plan in under one minute.
- User can find the full itinerary quickly.
- User can recover missed important activities.
- User trusts that changes are saved and restorable.
- User can export a backup before and during the trip.

## 9. Design Direction

The app should feel like a mobile travel companion.

Style direction:

- Mobile-first layout
- Strong Home dashboard
- Clear Planner tab
- Dark mode and light mode both fully readable
- Rounded cards
- Bottom navigation
- Floating assistant
- Gradient placeholders until real images are available
- Minimal clutter on Home
- More detailed tools inside Planner/Profile

## 10. Future Development Parking Lot

These are valuable but not needed for the MVP:

- Real AI assistant
- External RAG suggestions
- Live restaurant hours
- Live weather API
- Live route planning
- Backend saved trips
- Shareable links
- User accounts
- Collaborative editing
- Native app
- Automatic trip generation
- Import from PDF/Excel/email/Notion
- Photo journal and post-trip memory mode
