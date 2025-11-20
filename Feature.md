# Mobile Mantual Cards 
## Goal

Create a **responsive, mobile-first card-based component** (single self-contained HTML file with inline CSS and vanilla JavaScript) that displays service/job-order records **only on screens ≤ 600px**. The component must include search, brand filter, pagination, and smooth mobile UX. All data is static and hardcoded (same dataset as the desktop version — 25+ job orders).

## Data

* Use a hardcoded array of **at least 25 job orders** inside the page. Each record must contain:

  * `plateNo` (string)
  * `brand` (string)
  * `jobCardId` (string)
  * `estDelivery` (ISO date string or formatted string)
  * `advisor` (string)

(You can reuse the 25-record dataset previously provided for the desktop table.)

---

## Visibility

* The entire component is **hidden on screens > 600px** via CSS media queries. It is **visible only on mobile** (≤ 600px).

---

## Layout & Styling

* Page container: background `#F1F3F7`, padding `16px`, min-height `100vh`.
* Card style:

  * Background: white `#FFFFFF`
  * Border-radius: `8px`
  * Padding: `16px`
  * Margin-bottom: `16px`
  * Box-shadow: `1px 1px 1px rgba(197,197,197,1)`
  * Tap-friendly (entire card clickable)
* Text styles inside card:

  * Plate No: bold, `font-size: 16px`
  * Brand: gray secondary header, `font-size: 14px`, color `#757575`
  * Job Card ID: small, `font-size: 13px`, prefix `ID:`
  * Advisor: `font-size: 13px`, prefix `Advisor:`
  * Est. Delivery Date: `font-size: 13px`, prefix `Est. Delivery Date:` and formatted like `16-Oct-2024`.
* Active/selected states use purple accent `#2A00B2` for highlights and buttons.

---

## Search

* A mobile search bar sits at the top of the component (full-width):

  * Height `44–48px`, white background, left search icon, placeholder **"Search Services..."**.
  * Filters in real-time (no submit button). Debounced (200–250ms) for performance.
  * Search fields: plateNo, brand, jobCardId, advisor (case-insensitive substring match).
  * When search or filter changes, **reset pagination to page 1**.

---

## Brand Filter Popover

* Filter button positioned at the top-right.
* Clicking opens a slide-in popover/modal overlay with:

  * White box, rounded corners `8px`, padding `16px`, shadow, and semi-transparent backdrop.
  * Dropdown select for **Brand**: options include **All** + unique brands from the dataset.
  * `Reset` button to clear the filter.
  * `Close (X)` to dismiss.
* While popover is open, **prevent body scrolling** (`document.body.style.overflow = 'hidden'`), restore on close.
* Selecting a brand filters results immediately.

---

## Pagination

* Fixed bottom pagination bar (position fixed at bottom): background `#F1F3F7`, padding `12px`, box-shadow, z-index.
* Shows current page / total pages (e.g. `1 / 3`) and Previous/Next arrow buttons.
* **10 cards per page** from the currently filtered dataset.
* Calculate `totalPages = Math.ceil(filtered.length / 10)`.
* Controls:

  * Previous (disabled on page 1)
  * Next (disabled on last page)
  * Display `pageNum / totalPages` in center
* When search or filter changes, **reset to page 1** and recalc pages.

---

## Empty state

* If no records match the current search/filter, show centered message:

  * **No records found** (bold)
  * Secondary helper text (smaller, muted)

---

## Interactions

* Clicking a card simulates navigation to service details (use `alert()` or `console.log()`):

  ```js
  alert('Navigate to: http://127.0.0.1:5500/dashboard/manual-time-entry/manual-time-add.html');
  ```
* All state (search query, selected brand, current page) is managed in-memory with JS variables.
* Keep scroll position where sensible; however, when changing pages, scroll to top of the cards container for clarity.

---

## Accessibility & UX

* Tap targets ≥ 40px, readable contrast.
* Keyboard-accessible controls where practical.
* Smooth transitions for popover and pager.

---

## Implementation Notes

* Provide the full implementation as a **single HTML file** with inline CSS and JavaScript.
* Use vanilla JS only (no frameworks).
* Debounce search input.
* Store the initial dataset into `localStorage.jobOrders` on first run so data persists if desired.
* Ensure all filtering and pagination operations are client-side and instantaneous.

---

## Example dataset snippet (use 25 records — expand as needed):

```js
[
{"plate": "KL07AB1234", "brand": "Toyota", "jobCard": "JC-001", "estDelivery": "2025-01-12", "advisor": "John Mathew"},
{"plate": "KL05CD5678", "brand": "Honda", "jobCard": "JC-002", "estDelivery": "2025-01-15", "advisor": "Anu George"},
{"plate": "KL22EF9821", "brand": "Ford", "jobCard": "JC-003", "estDelivery": "2025-01-18", "advisor": "Rahul Nair"},
{"plate": "KL10GH4432", "brand": "Hyundai", "jobCard": "JC-004", "estDelivery": "2025-01-20", "advisor": "Sneha Jose"},
{"plate": "KL03JK2211", "brand": "Kia", "jobCard": "JC-005", "estDelivery": "2025-01-22", "advisor": "Vishnu Lal"},
{"plate": "KL15LM3344", "brand": "Mahindra", "jobCard": "JC-006", "estDelivery": "2025-01-25", "advisor": "Deepa Varma"},
{"plate": "KL08NP7788", "brand": "Tata", "jobCard": "JC-007", "estDelivery": "2025-01-26", "advisor": "Joseph Paul"},
{"plate": "KL40QR1299", "brand": "Suzuki", "jobCard": "JC-008", "estDelivery": "2025-01-28", "advisor": "Linda Maria"},
{"plate": "KL11ST4455", "brand": "Toyota", "jobCard": "JC-009", "estDelivery": "2025-02-01", "advisor": "Hari Mohan"},
{"plate": "KL29UV6677", "brand": "Honda", "jobCard": "JC-010", "estDelivery": "2025-02-03", "advisor": "Amal Roy"},
{"plate": "KL17WX8899", "brand": "Ford", "jobCard": "JC-011", "estDelivery": "2025-02-05", "advisor": "Sana Biju"},
{"plate": "KL12YZ1122", "brand": "Hyundai", "jobCard": "JC-012", "estDelivery": "2025-02-07", "advisor": "Kevin Thomas"},
{"plate": "KL06AA3344", "brand": "Kia", "jobCard": "JC-013", "estDelivery": "2025-02-10", "advisor": "Alwin James"},
{"plate": "KL19BB5566", "brand": "Mahindra", "jobCard": "JC-014", "estDelivery": "2025-02-12", "advisor": "Riya Cherian"},
{"plate": "KL13CC7788", "brand": "Tata", "jobCard": "JC-015", "estDelivery": "2025-02-14", "advisor": "Dileep P"},
{"plate": "KL02DD9900", "brand": "Suzuki", "jobCard": "JC-016", "estDelivery": "2025-02-16", "advisor": "Nikhil Das"},
{"plate": "KL20EE2211", "brand": "Toyota", "jobCard": "JC-017", "estDelivery": "2025-02-18", "advisor": "Sharon V"},
{"plate": "KL14FF4433", "brand": "Honda", "jobCard": "JC-018", "estDelivery": "2025-02-20", "advisor": "Julie Thomas"},
{"plate": "KL09GG6655", "brand": "Ford", "jobCard": "JC-019", "estDelivery": "2025-02-22", "advisor": "Mathew Jose"},
{"plate": "KL28HH8877", "brand": "Hyundai", "jobCard": "JC-020", "estDelivery": "2025-02-24", "advisor": "Sandra Paul"},
{"plate": "KL34II9988", "brand": "Kia", "jobCard": "JC-021", "estDelivery": "2025-02-27", "advisor": "Freddy K"},
{"plate": "KL04JJ1100", "brand": "Mahindra", "jobCard": "JC-022", "estDelivery": "2025-03-01", "advisor": "Merin John"},
{"plate": "KL23KK3322", "brand": "Tata", "jobCard": "JC-023", "estDelivery": "2025-03-04", "advisor": "Joel Antony"},
{"plate": "KL33LL5544", "brand": "Suzuki", "jobCard": "JC-024", "estDelivery": "2025-03-06", "advisor": "Rose Alex"},
{"plate": "KL26MM7766", "brand": "Toyota", "jobCard": "JC-025", "estDelivery": "2025-03-08", "advisor": "Rahul KP"}
]
```

---
## Image
<img src='./assets/Screenshot 2025-11-20 142455.png'>
<img src='./assets/Screenshot 2025-11-20 142428.png'>
<img src='./assets/Screenshot 2025-11-20 142524.png'>

