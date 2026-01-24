---
layout: page
title: Technical Documentation for Break Feature in OCS Calendar
search_exclude: True
toc: True
permalink: /blogs/break_documentation/
categories: ['CSA Classwork']
---

# Frontend:

## Overview

The break feature is a calendar functionality that allows users to designate specific dates as "break days" (such as holidays, teacher planning days, or scheduled breaks). When a date is marked as a break, any events scheduled on that day are automatically moved to the next non-break day, preventing scheduling conflicts during designated break periods.

---

## Feature Description

### What Does the Break Feature Do?

1. **Break Day Declaration**: Users can click on any calendar date and select "Make Break" to designate that date as a break day
2. **Break Naming**: Each break requires a name (e.g., "Winter Break", "Spring Break", "Professional Development Day")
3. **Break Description**: Users can optionally add a description for context
4. **Automatic Event Rescheduling**: When a break is created, all events on that day are automatically moved to the next available non-break day
5. **Break Visualization**: Break days are displayed with a distinct dark gray (#2a2a2a) background to differentiate them from regular events
6. **Break Management**: Users can delete break days, which presumably moves events back or handles them appropriately
7. **Break Prevention**: The system prevents creating multiple breaks on the same date

---

## Frontend Architecture & Code Components

### 1. **State Management**

```javascript
let allEvents = [];        // Global array storing all calendar events and breaks
let currentFilter = null;  // Tracks the active class filter (CSA, CSP, CSSE, or null)
let currentEvent = null;   // Currently selected event in the modal
let isAddingNewEvent = false; // Flag to distinguish new event creation from editing
```

**Purpose**: These variables maintain the state of the calendar application, tracking which events are loaded, what's currently displayed, and what the user is doing.

### 2. **Data Fetching Functions**

#### `request()`
- **Purpose**: Fetches calendar events from `/api/calendar/events`
- **Returns**: Promise resolving to array of calendar events
- **Error Handling**: Returns null on failure, logs errors to console

#### `getAssignments()`
- **Purpose**: Fetches assignment data from `/api/assignments/`
- **Returns**: Promise resolving to assignment array
- **Error Handling**: Returns null on failure
- **Note**: New function integrated to fetch assignment data alongside calendar events

#### `getBreaks()`
- **Purpose**: Fetches break data from `/api/calendar/breaks`
- **Returns**: Promise resolving to array of break events
- **Error Handling**: Returns empty array on failure
- **Integration**: Specifically designed to retrieve all scheduled breaks from the backend

### 3. **Break Utility Functions**

#### `isBreakDay(dateString)`
```javascript
function isBreakDay(dateString) {
    return allEvents.some(event => event.isBreak && event.start === dateString);
}
```
- **Purpose**: Checks if a given date has a break scheduled
- **Returns**: Boolean (true if date is a break day, false otherwise)
- **Usage**: Prevents duplicate breaks on the same date

#### `getBreakName(dateString)`
```javascript
function getBreakName(dateString) {
    const breakEvent = allEvents.find(event => event.isBreak && event.start === dateString);
    return breakEvent ? breakEvent.breakName : null;
}
```
- **Purpose**: Retrieves the name of a break on a specific date
- **Returns**: Break name string or null if no break exists
- **Usage**: Used for displaying break information to users

### 4. **Data Aggregation: `handleRequest()`**

This is the central hub for loading all calendar data. It uses `Promise.all()` to fetch from three endpoints simultaneously:

```javascript
Promise.all([request(), getAssignments(), getBreaks()])
    .then(([calendarEvents, assignments, breaks]) => {
        // Process all three types of data
    });
```

**Processing Flow**:

1. **Calendar Events Processing**:
   - Extracts priority from event title (format: `[P0]`, `[P1]`, `[P2]`, `[P3]`)
   - Assigns color based on priority (red for P0, orange for P1, yellow for P2, green for P3)
   - Falls back to class-based colors (CSP: blue, CSSE: green) if no priority detected
   - Adds `isBreak: false` to distinguish from break events
   - Stores in `allEvents` with full event metadata

2. **Assignments Processing**:
   - Parses due dates from format `MM/DD/YYYY`
   - Converts to standardized date format
   - Assigns orange color (`#FFA500`) to all assignments
   - Marks with `isBreak: false`

3. **Breaks Processing**:
   - Creates special break event objects
   - Assigns dark gray color (`#2a2a2a`)
   - Sets `isBreak: true` for identification
   - Stores break name for reference
   - Applies `fc-event-break` CSS class for styling

### 5. **Calendar Rendering: `displayCalendar(events)`**

Initializes the FullCalendar library with:

**Toolbar Configuration**:
- Navigation buttons (prev, next, today)
- Custom class filter buttons (All, CSA, CSP, CSSE)
- View options (Month, Week, Day)

**Event Click Handler**:
- Populates modal with event details
- **Break Event Logic**: For break events, only shows the delete button (prevents editing breaks)
- **Regular Event Logic**: Shows both edit and delete buttons for normal events
- Disables period and priority fields for viewing

**Date Click Handler** (Key for break creation):
```javascript
dateClick: function (info) {
    const selectedDate = formatDate(info.date);
    
    // CRITICAL: Check if date already has a break
    if (isBreakDay(selectedDate)) {
        alert(`There is already a break on ${formatDisplayDate(info.date)}`);
        return;
    }
    
    // Display modal for new event/break creation
    document.getElementById("makeBreakButton").style.display = "inline-block";
    // ... additional modal setup
}
```

**Key Feature**: The date click handler prevents creating multiple breaks on the same date through the `isBreakDay()` check.

### 6. **Event Filtering: `filterEventsByClass(className)`**

```javascript
function filterEventsByClass(className) {
    let filtered = allEvents;
    if (className) {
        // CRITICAL: Include breaks regardless of filter
        filtered = allEvents.filter(event => event.isBreak || event.period === className);
    }
    // Sort with breaks first, then by priority
    return filtered.sort((a, b) => { ... });
}
```

**Logic**:
1. If no filter: return all events
2. If filter active: return breaks PLUS events matching the class filter
3. Sort with breaks always appearing first, followed by events sorted by priority

**Design Rationale**: Breaks are always visible regardless of class filter because they affect scheduling across all classes.

### 7. **Break Creation: `makeBreakButton.onclick`**

This handler implements the complete break creation workflow:

**Step 1: Validation**
```javascript
if (!breakDate) {
    alert("Please select a date for the break!");
    return;
}
if (!breakTitle) {
    alert("Please enter a name for the break!");
    return;
}
if (isBreakDay(breakDate)) {
    alert(`There is already a break on...`);
    return;
}
```

**Step 2: User Confirmation**
```javascript
const confirmation = confirm(
    `Are you sure you want to make ${formatDisplayDate(localDate)} 
    a break day with the name "${breakTitle}"? 
    Events on this day will be moved to the next non-break day.`
);
```
- Informs user about automatic event rescheduling
- Allows user to cancel before submission

**Step 3: API Call**
```javascript
fetch(`${javaURI}/api/calendar/breaks/create`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
        date: breakDate,
        name: breakTitle,
        description: breakDescription,
        moveToNextNonBreakDay: true  // Triggers automatic rescheduling
    }),
})
```

**Step 4: Response Handling**
- On success: Display success alert, close modal, refresh calendar via `handleRequest()`
- On failure: Display error message with backend response details
- Logging for debugging: `console.log()` calls track the break creation payload and response

### 8. **Modal UI Components**

The modal includes:
- **Event Title Display**: Shows "Add New Event" for new items
- **Date Input**: Read-only display with hidden date picker for editing
- **Title Input**: `contentEditable` div that switches between display and edit modes
- **Description Input**: `contentEditable` div supporting HTML formatting
- **Class Selector**: Dropdown disabled for viewing, enabled during break creation
- **Priority Selector**: Only visible for regular events, hidden for breaks
- **Action Buttons**:
  - `saveButton`: Saves new event/break (shows only during creation)
  - `makeBreakButton`: Creates break from event data (shows only during creation)
  - `editButton`: Enables edit mode (hides for breaks)
  - `deleteButton`: Deletes event or break (shows for all)

### 9. **Styling & Visualization**

**CSS Classes & Colors**:
```css
.fc-event-break { background-color: #2a2a2a; border-color: #1a1a1a; }
.fc-daygrid-day.break-day { background-color: #2a2a2a; }
.priority-p0 { background-color: #dc2626; } /* Red */
.priority-p1 { background-color: #ea580c; } /* Orange */
.priority-p2 { background-color: #ca8a04; } /* Yellow */
.priority-p3 { background-color: #16a34a; } /* Green */
```

**Theme Integration**: Calendar uses CSS custom properties:
- `var(--bg-0)`: Primary background
- `var(--bg-1)`: Secondary background (alternating rows)
- `var(--bg-2)`: Header background
- `var(--accent)`: Accent color for borders
- `var(--text)`: Text color

---

## User Experience Flow

### Creating a Break
1. User clicks on a calendar date
2. Modal opens with "Add New Event" form
3. User enters break name in title field
4. User optionally adds description
5. User clicks "Make Break" button
6. Confirmation dialog appears with details
7. On confirmation, API creates break and reschedules events
8. Calendar refreshes showing break on designated date
9. Success message confirms completion

### Viewing Breaks
1. Break days appear with dark gray styling (#2a2a2a)
2. Break name is displayed as event title with "Break:" prefix
3. Clicking a break shows description and only delete option
4. Breaks remain visible across all class filters

### Deleting Breaks
1. Click on break event
2. Click "Delete Event" button
3. Confirm deletion
4. API removes break and handles rescheduling
5. Calendar updates

---

## Technical Integration Points

### Backend Dependencies
- `/api/calendar/events`: Fetch calendar events
- `/api/calendar/breaks`: Fetch all breaks
- `/api/calendar/breaks/create`: Create new break
- `/api/calendar/delete/{id}`: Delete event/break
- `/api/assignments/`: Fetch assignments

### FullCalendar Integration
- Version: 5.11.0
- Event objects include:
  - `id`: Unique identifier
  - `title`: Display name (prefixed with "Break:" for breaks)
  - `start`: Date string (YYYY-MM-DD format)
  - `color`: Hex color for event display
  - `isBreak`: Boolean flag
  - `period`: Class assignment (null for breaks)
  - `description`: Full event description
  - `breakName`: Original break name (for breaks)
  - `classNames`: CSS classes for styling

### Data Format
- **Dates**: ISO format (YYYY-MM-DD)

---

# Backend:

## Overview
The calendar breaks API has been fully implemented with support for creating, updating, deleting, and querying calendar breaks. Each break can have a custom name and description, and events on a break day can be automatically moved to the next non-break day.

## API Endpoints

### 1. Create Break
**Endpoint:** `POST /api/calendar/breaks/create`

**Request Body:**
```json
{
  "date": "2026-01-27",
  "name": "Winter Break",
  "description": "Two week winter break",
  "moveToNextNonBreakDay": true
}
```

**Response:**
```json
{
  "success": true,
  "message": "Break created successfully",
  "break": {
    "id": 1,
    "date": "2026-01-27",
    "name": "Winter Break",
    "description": "Two week winter break"
  }
}
```

**Features:**
- Stores custom break name (not defaulting to "Break")
- Stores break description
- Supports `moveToNextNonBreakDay` flag:
  - When `true`: Events on the break date are moved to the next non-break day
  - Automatically calculates the next non-break day by checking if subsequent dates have breaks
  - All event properties are preserved (title, description, type, period)
- Transaction-safe: all operations succeed or fail together
- Validates date format and name
- Prevents duplicate breaks on the same date

### 2. Get All Breaks
**Endpoint:** `GET /api/calendar/breaks/`

**Response:**
```json
[
  {
    "id": 1,
    "date": "2026-01-27",
    "name": "Winter Break",
    "description": "Two week winter break"
  },
  {
    "id": 2,
    "date": "2026-01-28",
    "name": "Spring Break Prep",
    "description": "Preparation for spring break"
  }
]
```

### 3. Get Breaks by Date
**Endpoint:** `GET /api/calendar/breaks/by-date?date=2026-02-01`

**Response:**
```json
[
  {
    "id": 3,
    "date": "2026-02-01",
    "name": "February Break",
    "description": "Month start break"
  }
]
```

### 4. Get Break by ID
**Endpoint:** `GET /api/calendar/breaks/{id}`

**Response:**
```json
{
  "id": 1,
  "date": "2026-01-27",
  "name": "Winter Break",
  "description": "Two week winter break"
}
```

### 5. Check if Break Day
**Endpoint:** `GET /api/calendar/breaks/is-break-day?date=2026-02-01`

**Response:**
```json
{
  "isBreakDay": true
}
```

### 6. Update Break
**Endpoint:** `PUT /api/calendar/breaks/{id}`

**Request Body:**
```json
{
  "name": "Updated Break Name",
  "description": "Updated description"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Break updated successfully",
  "break": {
    "id": 1,
    "date": "2026-01-27",
    "name": "Updated Break Name",
    "description": "Updated description"
  }
}
```

### 7. Delete Break by ID
**Endpoint:** `DELETE /api/calendar/breaks/{id}`

**Response:**
```json
{
  "success": true,
  "message": "Break deleted successfully"
}
```

**Note:** When a break is deleted, events that were moved to the next day are NOT automatically moved back. Users can manually reschedule if needed.

## Database Schema

### calendar_breaks Table
```sql
CREATE TABLE calendar_breaks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    date DATE NOT NULL,
    name VARCHAR(255) NOT NULL DEFAULT 'Break',
    description TEXT
);
```

**Fields:**
- `id`: Unique identifier (auto-generated)
- `date`: Date of the break (format: YYYY-MM-DD)
- `name`: Custom name for the break (e.g., "Winter Break", "Holiday")
- `description`: Optional description of the break

## Implementation Details

### Entity: CalendarBreak
- **File:** `src/main/java/com/open/spring/mvc/calendarBreak/CalendarBreak.java`
- **Table:** `calendar_breaks`
- **Fields:** id, date, name, description
- **Constructors:** Multiple overloads for flexible initialization

### Service: CalendarBreakService
- **File:** `src/main/java/com/open/spring/mvc/calendarBreak/CalendarBreakService.java`
- **Key Methods:**
  - `createBreak()`: Creates a new break and optionally moves events
  - `updateBreak()`: Updates break name and description
  - `deleteBreakById()`: Deletes break by ID
  - `deleteBreakByDate()`: Deletes break by date
  - `findNextNonBreakDay()`: Finds the first date without a break
  - `isBreakDay()`: Checks if a date is a break day
  - `getBreaksByDate()`: Gets breaks for a specific date
  - `getAllBreaks()`: Gets all breaks
  - `getBreakById()`: Gets break by ID

### Controller: CalendarBreakController
- **File:** `src/main/java/com/open/spring/mvc/calendarBreak/CalendarBreakController.java`
- **Base Path:** `/api/calendar/breaks`
- **Features:**
  - Comprehensive error handling with appropriate HTTP status codes
  - Input validation for date format and required fields
  - JSON request/response formatting
  - Proper separation from CalendarEventController endpoints

### Repository: CalendarBreakRepository
- **File:** `src/main/java/com/open/spring/mvc/calendarBreak/CalendarBreakRepository.java`
- **Query Methods:**
  - `findByDate()`: Retrieves breaks by date
  - `findAll()`: Retrieves all breaks
  - `findById()`: Retrieves break by ID

## Key Features

### 1. Next Non-Break Day Logic
When creating a break with `moveToNextNonBreakDay: true`:
- The system checks if the next day has a break
- If yes, it continues checking subsequent days
- Returns the first date without a break
- Supports up to 365 days ahead
- All events are moved while preserving their properties

### 2. Transaction Safety
- All operations are marked with `@Transactional`
- Break creation and event rescheduling happen atomically
- All succeed or all fail together

### 3. Input Validation
- Date format validation (YYYY-MM-DD)
- Break name validation (cannot be empty or null)
- Duplicate break prevention on same date
- Comprehensive error messages

### 4. Error Handling
- 400 Bad Request: Invalid input (date format, empty name)
- 404 Not Found: Break doesn't exist
- 500 Internal Server Error: Server errors with descriptive messages

## Example Usage

### Creating a Break with Multiple Consecutive Days
```bash
# Create break on 2026-01-27
curl -X POST http://localhost:8585/api/calendar/breaks/create \
  -H "Content-Type: application/json" \
  -d '{
    "date": "2026-01-27",
    "name": "Winter Break",
    "description": "Two week winter break",
    "moveToNextNonBreakDay": true
  }'

# Create another break on 2026-01-28
curl -X POST http://localhost:8585/api/calendar/breaks/create \
  -H "Content-Type: application/json" \
  -d '{
    "date": "2026-01-28",
    "name": "Winter Break Continuation",
    "description": "Second week of winter break",
    "moveToNextNonBreakDay": true
  }'

# Now events from 2026-01-27 move to 2026-01-29 (skipping 2026-01-28)
# And events from 2026-01-28 move to 2026-01-29
```

### Checking Multiple Dates
```bash
# Check if 2026-01-27 is a break day
curl -X GET "http://localhost:8585/api/calendar/breaks/is-break-day?date=2026-01-27"
# Response: {"isBreakDay":true}

# Check if 2026-01-29 is a break day
curl -X GET "http://localhost:8585/api/calendar/breaks/is-break-day?date=2026-01-29"
# Response: {"isBreakDay":false}
```

## Migration Notes

### From Previous Implementation
- **Changed:** `title` field → `name` field
- **Added:** `description` field to CalendarBreak entity
- **Changed:** Base endpoint path from `/api/calendar` to `/api/calendar/breaks`
- **Changed:** Some endpoint paths to avoid conflicts with CalendarEventController
  - DELETE endpoint changed from `/delete_break/{id}` to `/{id}`
  - POST endpoint changed from `/create_break` to `/create`
  - PUT endpoint: new endpoint at `/{id}`
  - GET all: changed from `/breaks` to `/`
  - GET by date: changed from `/breaks/by-date` to `/by-date`
