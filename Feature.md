# Mobile Holiday Management — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) optimized for **mobile screens below 600px** that implements a **Holiday Management View** using `localStorage` for persistence. The component must follow a clean, purple-accent theme and provide search, filtering, edit/delete, and pagination controls tailored for mobile UX.

---

## Container & Page Layout

* Page container: `padding: 16px`, background `#F1F3F7`, `min-height: 100vh`.
* Mobile-first design targeting screens `< 600px`.

---

## Header Controls

* Top header: `display: flex; justify-content: space-between; margin-bottom: 16px;`

* **Left:** Two toggle switches for **SUN** and **SAT**:

  * Inline-flex, gap `4px`, label font-size `14px`, color `#404040`.
  * Custom toggle checkbox: rounded toggle `width: 44px; height: 24px;`.
  * Unchecked background `#ccc`; checked background `#2196f3`.
  * Slider circle `20px`, white, transition `0.3s`.
  * Toggle state is read from and saved to `localStorage` key `weekdays` (JSON array of objects `{dayNumber, active}` where `0` is Sunday and `6` is Saturday).
  * On change update `weekdays` in `localStorage`, update local weekdays state and UI.
  * Label margin-left approx `-0.2` for tight spacing.

* **Right:** Two icon buttons:

  * **Filter** button (40×40 circle). On click open filter popover/overlay (`filterAnchorEl` state).
  * **Add** button (40×40 circle). On click navigate to `/app/settings/holiday/config` via `window.location.href`.
  * Both buttons: hover opacity `0.7`.

---

## Search Input

* Full-width search below header:

  * `width: 100%`, `height: 40px`, padding `0 12px 0 40px`, border `2px solid #D2D5DA`, border-radius `6px`, background `#FFFFFF`, font-size `14px`.
  * Left-positioned search icon (`position: absolute; left: 12px; top: 50%; transform: translateY(-50%);`).
  * Placeholder: **"Search holidays..."**.
  * Value bound to `searchQuery` state; on change filter displayed cards and reset `currentPage` to 1.

---

## Holiday Cards List

* Vertical stack of cards with `gap: 16px`.
* Each card style: background `#FFFFFF`, border-radius `8px`, padding `16px`, box-shadow `0 2px 4px rgba(0,0,0,0.1)`.

### Card Header

* `display:flex; justify-content: space-between; align-items: center;`
* **Left:** Event name (`h6`): font-size `18px`, bold, max-width `200px`, ellipsis overflow.

  * When editing (`isEditing` true) show input field instead (200px wide, 32px high) bound to `holiday.name`.
* **Right:** Action icons container (`display:flex; gap:8px`):

  * Editing state shows **Save** (green) and **Cancel** (red-ish) icons.
  * Delete state shows **Delete** (red) and **Cancel** icons.
  * Default shows **Edit** (blue) and **Delete** icons.
  * Edit is disabled for past holidays (`status === "Over"`) — gray, `cursor:not-allowed`, tooltip `Cannot edit past holidays`.

### Card Content

* Grid layout with gap `12px`.
* **Start Date** and **End Date** sections:

  * If editing: show native `type=date` inputs (height 42px, border `2px solid #D2D5DA`, border-radius `6px`). End Date `min` bound to Start Date.
  * If not editing: show label `Start Date:` / `End Date:` and formatted date value using `config.globalisation.dateFormat` (fallback `DD-MM-YYYY`).
* **Status chip:** small rounded badge showing **Over** (red `#FF0000`), **Upcoming** (orange `#FFA500`), or **Ongoing** (green `#008000`) determined by comparing today with start/end dates.

---

## Empty State

* If filtered results are empty show a centered card:

  * `h6`: "No records found" (18px, `#404040`)
  * `p`: "Try adjusting your search or filter criteria" (14px, `#666`)

---

## Filter Popover (Mobile)

* Fullscreen overlay (`position: fixed; top:0; left:0; width:100vw; height:100vh; background: rgba(0,0,0,0.5); z-index:1000`) that can be closed by tapping the backdrop.
* Centered filter panel (`width:320px; max-height:80vh; background:#FFF; border-radius:8px; padding:16px`) with:

  * Header: **FILTERS** label and **RESET** button that clears date filters and resets `currentPage`.
  * Close button to dismiss.
  * Body: two date inputs (Start, End). Changing dates immediately filters displayed data; End date `min` bound to Start date.
* When open, apply scroll lock: `document.body.style.overflow = 'hidden'`; restore on close.

---

## Pagination (Fixed Bottom Bar)

* Fixed bottom bar (`position: fixed; bottom:0; left:0; right:0; background:#F1F3F7; padding:12px 0; z-index:100`) with controls centered.
* Previous/Next circular buttons (32px) with disabled state when at edges (opacity 0.5, `cursor:not-allowed`).
* Page number buttons (32px circular) showing up to 5 pages with ellipses for larger ranges. Active page background `#2196f3` with white text.
* Only show when `totalPages > 0`.

---

## Filtering & Pagination Logic

1. Build `filteredData` by applying in order:

   * `searchQuery` (case-insensitive) against `holiday.name`, formatted `start_date`, and formatted `end_date`.
   * Date range filters (`filterDates.startDate` / `filterDates.endDate`).
2. Compute `totalPages = Math.ceil(filteredData.length / rowsPerPage)`.
3. Slice current page: `filteredData.slice((currentPage-1)*rowsPerPage, currentPage*rowsPerPage)`.
4. Render cards for the sliced array.

---

## Edit / Delete Flows

* **Navigation Requirement**: When clicking the **Edit** or **Delete** icons on a holiday card, the user must be navigated to dedicated pages:

  * Edit → `/app/settings/holiday/edit.html?id={holidayId}`
  * Delete → `/app/settings/holiday/delete.html?id={holidayId}`
    These navigations should occur immediately on icon click before entering any inline edit/delete mode.

---

## Toasts

* `createToast(message, type)` renders top-center toasts with green (`#16A34A`) for success and red (`#DC2626`) for error, auto-dismiss after 3s with fade animations.

---

## UX Details & Accessibility

* Inputs and controls use clear labels, proper touch targets, and accessible aria attributes.
* Tooltips via `title` attribute for disabled actions (e.g., "Cannot edit past holidays").
* Backdrop/tap-to-close behavior for popovers.

---

## Implementation Notes

* All localStorage reads/writes wrapped in `try/catch` with toasts on exceptions.
* Dates stored in `localStorage` as `YYYY-MM-DD` strings.
* Mobile layout reserves bottom padding to avoid content being hidden behind fixed pagination.
* Console debug logs helpful events (edit, save, delete, filter changes).

---

## Output

Produce a single self-contained HTML file with inline CSS and JavaScript that implements the Mobile Holiday Management View per the specification above.

## Sample Mock Data

```js
[
  {
    "id": "HLD-001",
    "title": "New Year’s Day",
    "type": "General",
    "startDate": "2025-01-01",
    "endDate": "2025-01-01",
    "description": "National public holiday marking the start of the year",
    "isActive": true
  },
  {
    "id": "HLD-002",
    "title": "Republic Day",
    "type": "General",
    "startDate": "2025-01-26",
    "endDate": "2025-01-26",
    "description": "Indian Republic Day celebration",
    "isActive": true
  },
  {
    "id": "HLD-003",
    "title": "Good Friday",
    "type": "General",
    "startDate": "2025-04-18",
    "endDate": "2025-04-18",
    "description": "Christian religious holiday",
    "isActive": true
  },
  {
    "id": "HLD-004",
    "title": "Eid al-Fitr",
    "type": "Special",
    "startDate": "2025-03-31",
    "endDate": "2025-04-01",
    "description": "Two-day special celebration at the end of Ramadan",
    "isActive": true
  },
  {
    "id": "HLD-005",
    "title": "Labour Day",
    "type": "General",
    "startDate": "2025-05-01",
    "endDate": "2025-05-01",
    "description": "International Workers’ Day",
    "isActive": true
  },
  {
    "id": "HLD-006",
    "title": "Onam",
    "type": "Special",
    "startDate": "2025-09-05",
    "endDate": "2025-09-08",
    "description": "Festival celebrated in Kerala",
    "isActive": true
  },
  {
    "id": "HLD-007",
    "title": "Diwali",
    "type": "Special",
    "startDate": "2025-10-20",
    "endDate": "2025-10-24",
    "description": "Festival of lights",
    "isActive": true
  },
  {
    "id": "HLD-008",
    "title": "Christmas",
    "type": "General",
    "startDate": "2025-12-25",
    "endDate": "2025-12-25",
    "description": "Christmas Day celebration",
    "isActive": true
  }
]
```
