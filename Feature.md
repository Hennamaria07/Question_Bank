# Task Overview

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) optimized for **mobile screens (≤ 600px)** that implements a **Task Overview** (job orders) page using a card-based layout. The UI must be mobile-first, touch-friendly, include search + filters + pagination, and implement the dialogs and flows described below.

**Reference image (local):**
`/mnt/data/1553f955-955f-4642-91f4-74dc45e7f61e.png`

---

## Visual & Layout Summary

* Page background: `#F1F3F7`. Page padding: `16px` left/right, `padding-top: 80px` (to clear fixed action buttons), `padding-bottom: 80px` (for fixed pagination).
* Cards: white `#FFFFFF`, border-radius `8px`, padding `16px`, margin-bottom `16px`, box-shadow `0 2px 4px rgba(0,0,0,0.1)`.
* Typography: Helvetica family. Tap targets ≥ 40px.
* All interactions show subtle transitions (scale on touch, shadow rise on active, slide/fade for popovers).

---

## Card content (mobile)

Each job order card shows:

* **Plate No** — top-left, bold (16px).
* **Brand** — below plate, gray subtitle (14px).
* **ID** — next line with prefix `ID: ` (13px).
* **Advisor** — `Advisor: ` (13px).
* **Est. Delivery Date** — `Est. Delivery Date: ` with dates formatted like `16-Oct-2024` (13px).
* Card tappable: clicking/tapping triggers alert:

  ```
  Navigating to: http://127.0.0.1:5500/dashboard/task/startservice.html
  ```
* Card `min-height` ensures consistent layout.
* The card with `jobCardId === "JC-2024-002"` is highlighted with light green background `#8ee7a3` (active session).

---

## Fixed action button row (top-right)

Positioned `top: 16px; right: 16px; z-index: 10` (absolute / fixed as appropriate). Buttons (display flex, gap 8px):

1. **Rejection** (rectangular)

   * Enabled when `rejectionCount > 0`.
   * Styles: blue `#2196f3` when enabled, light-blue `#ADD8E6` when disabled; white text; padding `8px 16px`; border-radius `6px`.
   * Red circular badge (20×20) at top-right of the button showing count `3`.
   * Click behavior:

     * If `count > 0`: alert `Navigating to rejection page with 3 rejections`.
     * If `count === 0`: alert `No rejections`.
   * **NOTE** (per spec): the rejection button should navigate to the (exact) URL:

     ```
     http://127.0.0.1:5500/http://127.0.0.1:5500/dashboard/rejection.html
     ```

     — this is a literal requirement from your spec; the implementation will respect it (or you can correct it later if you meant a single URL).

2. **QR Scanner** (circular)

   * 40×40, white background, border `1px solid #D2D5DA`, icon gray `#666666`.
   * On tap: `alert("QR Scanner clicked")`.

3. **Filter** (circular)

   * Opens Mobile Filter Dialog (popover/modal).

4. **Day End Task** (circular)

   * Background green `#34C759` when active session exists; gray `#9E9E9E` otherwise.
   * If active (green): clicking opens Day End Confirmation Dialog (flows below).
   * If inactive (gray): clicking shows `alert("No active session to end")`.

*Buttons have hover/touch feedback (scale 0.95) and tooltips via `title` attribute.*

---

## Search bar

* Positioned below action buttons (use `margin-top: 60px` to clear fixed header).
* Full-width (page padding minus), white background, border `1px solid #D2D5DA`, border-radius `8px`, padding `12px 16px`, height `48px`.
* Left adornment: magnifying glass icon (gray `#666666`).
* Placeholder: `"Search Services..."`.
* Filtering: real-time (debounced ~200–250ms), case-insensitive match against plate, brand, job card ID, and advisor name.
* Shows result count below in gray: `"Showing X of Y results"`.

---

## Mobile Filter Dialog / Popover

* Opens anchored top-right at `top: 60px; right: 16px`.
* Backdrop: full-screen `rgba(0,0,0,0.4)`, closes on click.
* Popover box: width `280px`, white background, border-radius `8px`, padding `16px`, shadow `0 4px 12px rgba(0,0,0,0.15)`.
* Header: `FILTERS` + blue `RESET` (clears filters & search).
* Brand filter:

  * Label `Brand`.
  * Native select with `All` + unique brands (from the 15 job orders).
  * On select: filter immediately.
* RESET returns brand to `All` and shows all cards.
* Close icon at top-right closes popover.

---

## Day End / Break dialogs

### Day End Confirmation Dialog

* Centered modal (backdrop rgba(0,0,0,0.5)).
* Box: width `90%` (max 350px), border-radius `12px`, padding `20px`.
* Title: `Confirm Day End Task`.
* Message: `Are you sure you want to end your day task?`.
* Buttons: **Yes** (blue) and **No** (white/gray).
* Yes → opens **Break Time Work Dialog**.
* No → closes and `alert("Day end cancelled")`.

### Break Time Work Dialog

* Centered modal similar style.
* Title: `Did you work during break time?` and subtitle `Worked Time during Breaks`.
* Two stacked inputs (mobile-first): **Hours** (0–23), **Minutes** (0–59).

  * Minutes input caps at 59 on input.
* Buttons: **Yes** and **No**.

  * Yes: if both inputs are 0/empty show red toast: `"Please enter valid worked hours or minutes"`.

    * If valid: `alert("Break time recorded: X hours Y minutes")` and close.
  * No: `alert("Break time skipped")` and close.
* Toast implementation: top-center, red background `#DC2626`, auto-dismiss 3s, animated.

All modals lock body scroll while open (`document.body.style.overflow = 'hidden'`), restore on close.

---

## Pagination (fixed bottom)

* Fixed bottom bar: background `#F1F3F7`, padding `12px 16px`, shadow `0 -2px 8px rgba(0,0,0,0.1)`, z-index `100`.
* Shows `"Page X of Y"` (12px gray) and centered pagination controls:

  * **Previous** / **Next** buttons (white when enabled, `#E0E0E0` when disabled).
  * Circular page buttons (32px): active `#2196f3` white text; inactive white border `1px solid #ddd`.
  * Max 5 visible page buttons; ellipsis if more pages.
* Items per page: **10**.
* Logic: totalPages = `Math.ceil(filteredData.length / 10)`; slice using `((page-1)*10, page*10)`.
* Smooth scroll-to-top when changing pages.

---

## Empty state

* When no results: centered message area (min-height 300px):

  * Title: `"No records found"` (18px, bold).
  * Subtitle: `"Try adjusting your search or filter criteria"` (14px, gray).
  * Optional search icon above.

---

## Interactions & behavior summary

* Search + Brand filter combine via chained `.filter()` calls.
* Only one popover/dialog open at a time.
* Debounced search (250ms).
* Maintain scroll position when filtering; smooth scroll to top when changing pages.
* Logs: `console.log` on major actions (open filter, page change, search query, modal open, day end actions).
* Prevent body scroll while popover/modal open.
* Alerts used for navigation placeholders and quick feedback.

---

## Special navigation note (per spec)

* Clicking the **Rejection** button will (per the requirement you gave) navigate to the literal URL:

```
http://127.0.0.1:5500/http://127.0.0.1:5500/dashboard/rejection.html
```

This looks like a duplicated URL — confirm if you want a single `http://127.0.0.1:5500/dashboard/rejection.html` instead. The implementation will use whichever you confirm; default will follow your literal instruction.

---

## Data — **exact 15 job orders (mock data)**

Use this array as the page dataset (the implementation should store it in a variable or in `localStorage.jobOrders` on first load):

```js
const jobOrders = [
  { plate: "KL-07-AB-1234", brand: "Toyota Camry", jobCardId: "JC-2024-001", advisor: "John Smith", estDelivery: "2024-10-16", isActive: false },
  { plate: "TN-09-CD-5678", brand: "Honda Accord", jobCardId: "JC-2024-002", advisor: "Sarah Johnson", estDelivery: "2024-10-17", isActive: true }, // active
  { plate: "MH-12-EF-9012", brand: "Maruti Swift", jobCardId: "JC-2024-003", advisor: "Michael Brown", estDelivery: "2024-10-18", isActive: false },
  { plate: "KA-01-GH-3456", brand: "Hyundai Creta", jobCardId: "JC-2024-004", advisor: "Emily Davis", estDelivery: "2024-10-19", isActive: false },
  { plate: "DL-08-IJ-7890", brand: "Tata Nexon", jobCardId: "JC-2024-005", advisor: "Robert Wilson", estDelivery: "2024-10-20", isActive: false },
  { plate: "UP-16-KL-2345", brand: "Ford EcoSport", jobCardId: "JC-2024-006", advisor: "John Smith", estDelivery: "2024-10-21", isActive: false },
  { plate: "RJ-14-MN-6789", brand: "Mahindra XUV500", jobCardId: "JC-2024-007", advisor: "Sarah Johnson", estDelivery: "2024-10-22", isActive: false },
  { plate: "GJ-01-OP-4567", brand: "Kia Seltos", jobCardId: "JC-2024-008", advisor: "Michael Brown", estDelivery: "2024-10-23", isActive: false },
  { plate: "MP-05-QR-1234", brand: "Nissan Magnite", jobCardId: "JC-2024-009", advisor: "Emily Davis", estDelivery: "2024-10-24", isActive: false },
  { plate: "HR-03-ST-5678", brand: "Renault Duster", jobCardId: "JC-2024-010", advisor: "Robert Wilson", estDelivery: "2024-10-25", isActive: false },
  { plate: "PB-10-UV-9012", brand: "Volkswagen Polo", jobCardId: "JC-2024-011", advisor: "John Smith", estDelivery: "2024-10-26", isActive: false },
  { plate: "WB-22-WX-3456", brand: "Skoda Rapid", jobCardId: "JC-2024-012", advisor: "Sarah Johnson", estDelivery: "2024-10-27", isActive: false },
  { plate: "AP-09-YZ-7890", brand: "MG Hector", jobCardId: "JC-2024-013", advisor: "Michael Brown", estDelivery: "2024-10-28", isActive: false },
  { plate: "TS-29-AB-2345", brand: "Jeep Compass", jobCardId: "JC-2024-014", advisor: "Emily Davis", estDelivery: "2024-10-29", isActive: false },
  { plate: "KL-14-CD-6789", brand: "Mahindra Thar", jobCardId: "JC-2024-015", advisor: "Robert Wilson", estDelivery: "2024-10-30", isActive: false }
];
```

* `estDelivery` dates stored as ISO `YYYY-MM-DD` strings; UI should format as `16-Oct-2024`.
* `isActive: true` marks the active session (Job `JC-2024-002`), applying the light-green background highlight.

---

## Implementation notes & tips

* Store `jobOrders` into `localStorage.jobOrders` on first run so the dataset persists.
* **Search**:

  ```js
  const q = query.trim().toLowerCase();
  const filtered = jobOrders.filter(j =>
    j.plate.toLowerCase().includes(q) ||
    j.brand.toLowerCase().includes(q) ||
    j.jobCardId.toLowerCase().includes(q) ||
    j.advisor.toLowerCase().includes(q)
  );
  ```
* **Brand filter**: derive unique brands from `jobOrders.map(j=>j.brand)` and populate dropdown.
* **Pagination**: `totalPages = Math.ceil(filtered.length / 10)`. Slice for the page.
* **Active card highlight**: `if (j.jobCardId === 'JC-2024-002')` apply `background: #8ee7a3`.
* **Dialogs**: create generic modal overlay element appended to `document.body` and lock scroll (`overflow: hidden`) while open.
* **Toast**: top-center floating notifications auto-dismiss after 3s.
* **Navigation simulation**: clicking a card shows `alert('Navigating to: http://127.0.0.1:5500/dashboard/task/startservice.html')`
* **Rejection button**: show badge `3` (hardcoded per spec); alert behavior as above; navigate to the literal doubled URL if you want exact spec behavior.

---

## Image
<img src='./assets/Screenshot 2025-11-20 141102.png'>
<img src='./assets/Screenshot 2025-11-20 141132.png'>
<img src='./assets/Screenshot 2025-11-20 141142.png'>
<img src='./assets/Screenshot 2025-11-20 141206.png'>