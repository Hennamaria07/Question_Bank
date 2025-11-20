# Mobile Vehicle Management List — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) optimized for **mobile screens (≤ 600px)** that implements a **Vehicle Management List** UI. The component must display vehicles as cards, support search, filters, pagination, actions, and an expandable job-card details panel. Use `localStorage` for the data source.

---

## Layout & Visuals

* Page background: `#F1F3F7` with side padding `16px` (mobile container). Reserve bottom padding `80px` to avoid overlapping pagination.
* Cards: white background, `border-radius: 8px`, `padding: 16px`, `margin-bottom: 16px`, `box-shadow: 0 2px 4px rgba(0,0,0,0.1)`.
* Fonts: `Helvetica, "Helvetica Neue", Arial, sans-serif`.
* Touch-friendly controls: minimum 40px tap targets.

---

## Card Content

Each vehicle card displays:

* **Plate Number** (title, 18px, bold)
* **Status dot** (25px colored circle) next to plate
* **Expand arrow** top-right toggles collapse/expand
* **Brand** line prefixed with `Brand: ` (14px)
* **VIN** line prefixed with `VIN: `
* **Owner** line prefixed with `Owner: ` (firstname + lastname)
* **Contact** line prefixed with `Contact: `
* **Action** row (prefixed `Action:`) with five icon buttons horizontally:

  * **Job Card** (wrench)
  * **Edit** (blue `#5B8FF9`) — navigates to the edit page or shows alert
  * **Delete** (red `#FE7062`) — asks confirmation or navigates
  * **History** (clock)
  * **QR Code** (shows alert `QR Code generation clicked for {plateNumber}`)

Actions trigger alerts and `console.log` for debug.

---

## Expand / Collapse

* Tapping the expand arrow or card toggles a collapsible section (only one card expanded at a time).
* Collapsed section shows **Current Job Card Details** or `No active job card` if none.
* When active, show:

  * Date Arrived (formatted `DD-MMM-YYYY`, e.g., `16-Oct-2024`)
  * Advisor name
  * Estimated Delivery date (formatted)
  * Status text
* Collapse/expand animated with `transition: height 300ms ease` for smooth UX.

---

## Top Action Row & Search

* Fixed action row (top-right aligned) with three circular icon buttons (40px):

  * **Filter** (FilterList icon) opens Mobile Filter Dialog
  * **Export** (download icon) shows alert `Exporting vehicle data...`
  * **Add** (plus icon) navigates to `/add/{userId}` and shows alert
* Search bar below action row:

  * Full width, white background, `border: 1px solid #D2D5DA`, `border-radius: 8px`, `height: 48px`, `padding: 12px 16px`.
  * Magnifying glass start adornment and placeholder `Search vehicles...`.
  * Filters plate, brand, VIN, owner, contact in real time with debounce.

---

## Mobile Filter Dialog

* Popover anchored to top-right (width `320px`) with backdrop (`rgba(0,0,0,0.4)`).
* Header: `FILTERS` and blue `RESET` button. Close `X` top-right.
* Two filters:

  * **Brand**: autocomplete search box with placeholder `Search Brand` (width 240px).
  * **Status**: native select (width 240px) with options:

    * All, Job card created, In-progress, On hold, Ready for delivery, Draft, None Active
* RESET clears filters and sets page to 1.
* Clicking outside backdrop closes dialog.

---

## Pagination (Fixed Bottom Bar)

* Fixed at bottom: `background: #F1F3F7`, padding `12px 16px`, `box-shadow: 0 -2px 8px rgba(0,0,0,0.1)`, `z-index: 100`.
* Shows `Page X of Y` (12px gray) and centered pagination controls:

  * Previous/Next buttons (white enabled, `#E0E0E0` disabled)
  * Circular page buttons (32px): active `#2196f3` white text, inactive transparent with border `1px solid #ddd`.
  * 10 cards per page; max 5 visible page buttons.

---

## Data & Storage

* Load 20 sample vehicles from `localStorage['vehicleAccounts']` (create if missing).
* Each vehicle record includes:

  * `id`, `plateNo`, `brand`, `model`, `vin`, `firstName`, `lastName`, `primaryContact`, `whatsapp`, `company`, `currentJobCard` (object or null), `status` (string)
* Provide 20 sample entries included in the implementation for testing.

---

## Filtering & Search Logic

* Combined filtering (search + brand + status): apply searchQuery (case-insensitive) across plate/brand/VIN/owner/contact then apply brand/status filters.
* Debounce search input (e.g., 250ms) to avoid excessive re-renders.
* Compute `totalPages = Math.ceil(filteredData.length / itemsPerPage)` and slice for current page.
* Update pagination when filters/search change and reset to page 1.

---

## UX Details

* Only one expanded card is allowed at a time (track `expandedCardId`).
* Loading spinner shown while fetching data (centered, rotating border animation).
* Status color mapping:

  * Yellow `#fffd00`, Green `#7EF782`, Orange `#ff4e00`, Blue, Red, Gray `#A3A3A3`.
  * Determine via job card status and estimated delivery vs. current date.
* Smooth transitions (300ms) on collapse, filter dialog, and pagination.
* Accessibility: buttons have `aria-label`, tooltips via `title`, large touch targets.

---

## Output

Produce a **single self-contained HTML file** implementing the above Mobile Vehicle Management List. The file should include:

* Inline CSS and JS
* 20 sample vehicle records in `localStorage` for immediate testing
* All interactions and alerts described above

---
## Image
<img src='./assets/Screenshot 2025-11-20 133438.png'>
<img src='./assets/Screenshot 2025-11-20 133458.png'>
<img src='./assets/Screenshot 2025-11-20 133513.png'>
<img src='./assets/Screenshot 2025-11-20 133531.png'>