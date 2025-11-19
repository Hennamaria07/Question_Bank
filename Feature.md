# Holiday Management

Create a **single self-contained HTML file** (HTML + inline CSS + vanilla JavaScript) implementing a **Holiday Management Page** that manages company holidays in `localStorage`. The page must provide a **clean, responsive, and interactive UI** with features for adding, editing, deleting, searching, filtering, and pagination of holidays.

---

## Container

* Card-style container:
  * Margin: `0 30px`
  * Padding: `20px`
  * Background: `#F1F3F7`
  * Border-radius: `15px`

---

## Toolbar

* Top-right toolbar includes:
  * **Add Icon** → navigates to `/app/settings/holiday/config`
  * **Weekday toggles** for SUN and SAT:
    * Medium switches
    * Checked state read from `localStorage.key "weekdays"` by `dayNumber === 0` (SUN) and `dayNumber === 6` (SAT)
    * Toggling updates `active` boolean in `localStorage`
  * **Search Box**:
    * Placeholder: `"Search holidays..."`
    * Width: 300px
    * Filters holidays by **name** or **formatted dates** as user types

---

## Holiday Table

* Responsive table:
  * Pale header: `#D0D4F2`
  * Uppercase, bold headings
  * Rounded first/last header corners
  * Alternating row backgrounds: odd `#F7F6FE`, even `#FFFFFF`
* Columns:
  * Event (200px)
  * Start Date (150px)
  * End Date (150px)
  * Status (computed)
  * Actions (edit/delete icons)
* Data loaded from `localStorage.holidays`
  * Each holiday object: `{_id, name, start_date, end_date}`
  * On load, augment entries with `isEditing` and `isDelete` flags

---

## Editing & Deleting

* **Inline Edit**:
  * Edit icon turns row into inputs and date pickers (formatted using config or fallback `DD-MM-YYYY`)
  * Cancel button restores original data
  * Save button validates:
    * `end_date >= start_date`
    * Updates `localStorage` on success
    * Shows green toast: `"Holiday updated successfully"`
  * Disabled Edit for past holidays shows tooltip: `"Cannot edit past holidays"`

* **Delete**:
  * Confirmation step
  * Removes holiday from `localStorage` and UI
  * Shows green success toast

---

## Status Calculation

* Status auto-calculated based on today’s date:
  * **Over** → `end_date < today` → red `#FF0000`
  * **Upcoming** → `start_date > today` → orange `#FFA500`
  * **Ongoing** → `start_date <= today <= end_date` → green `#008000`

---

## Filter Popover

* Opens via filter icon
* Width: 220px
* Contains:
  * Start Date and End Date inputs
  * RESET button clears filters
* While open:
  * Page body scroll-locked

---

## Pagination

* Client-side pagination:
  * Rows-per-page selector: 10 / 20 / 30 / 40
  * Previous / Next buttons (disabled at edges, reduced opacity)
  * Page indicator
  * `"Showing X–Y of Z entries"` text
* Filtering or search resets page to 1

---

## IDs & Data Handling

* Unique IDs generated as `Date.now() + Math.random()`
* LocalStorage reads/writes wrapped in `try/catch` using `JSON.parse` / `JSON.stringify`
* Graceful fallbacks if storage is missing or malformed
* Centered loading spinner (~500ms) while reading localStorage
* Display `"No holidays found"` if array is empty

---

## Date Formatting

* Convert stored `YYYY-MM-DD` strings into display format `DD-MM-YYYY`
* Supports configurable date format from config

---

## Controls & Accessibility

* Inputs have clear validation and focus states (2px blue outline when editing)
* Tooltips on disabled actions
* Toast notifications:
  * Top-center, auto-dismiss after 3s
  * Success: green
  * Error: red
* Fully responsive layout:
  * Above 1020px → full table layout
  * Below 1020px → stacked blocks with `data-label` labels per field
* Solid concrete styling for padding, borders (`2px solid #D2D5DA` on inputs)

---

## Summary of Features

* Toolbar with Add, Weekday toggles, and Search
* Responsive, card-style container
* Table with alternating row colors, rounded headers
* Inline edit with date validation
* Delete with confirmation
* Status colored based on dates
* Filter popover with date range
* Client-side pagination
* Toast notifications for success/error
* Loading spinner and empty-state handling
* Fully responsive layout with mobile-friendly stack
* Robust localStorage error handling


## Image
<img src='./assets/Screenshot 2025-11-19 161950.png'>
<img src='./assets/Screenshot 2025-11-19 162030.png'>
<img src='./assets/Screenshot 2025-11-19 162100.png'>