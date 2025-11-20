# Mobile Job History

## Goal

Build a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) optimized for **mobile screens below 800px** that implements a **Job History** view. The component must use `localStorage` for data, provide search and filtering, support pagination and PDF invoice generation, and present a clean mobile-first layout with accessible modals and toasts.

---

## Header

* Title: **History** (font-size 20px, font-weight bold, color `#333333`, margin-bottom `20px`).
* Top-right **Filter** icon button opens mobile filter popover anchored to the button.
* Filter popover: width `220px`, border-radius `8px`, padding `16px`, white background, anchored bottom-right. Contains "FILTERS" header, a **RESET** button, Close icon, and two date inputs for **Arrival Date** and **Delivered Date** (native `type=date`, styled, border `2px solid #D2D5DA`).

---

## Search

* Full-width search input below header with Search icon start adornment.
* Style: white background, height `40px`, border-radius `4px`, placeholder **"Search services..."**, margin-bottom `16px`.
* Typing filters job cards (matching name, dates, amounts) and resets pagination to page 1.

---

## Job History Cards

* Vertical stack of cards (gap `16px`).
* Card style: background `#f2f2f2`, border-radius `8px`, padding `15px`, box-shadow `0 2px 4px rgba(0,0,0,0.1)`.

### Card Header

* Left: **Job History** title (bold).
* Right: **PDF icon button** (red `#e74c3c`) with tooltip **"Generate Invoice PDF"** — opens Invoice modal.

### Card Body

* Grid (label-value pairs) showing:

  * **Arrival Date** (formatted)
  * **Delivery Date** (formatted)
  * **Total Hours** (HH:MM)
  * **Total Amount** (currency formatted)
* Display uses `flex` with `justify-content: space-between`, font-size `14px`.

### Empty State

* If no records, show centered card: **"No history available"** (height `200px`, font-size `18px`).

---

## Pagination (Fixed Bottom Bar)

* Fixed bottom bar: `position: fixed; bottom:0; left:0; right:0; background:#F1F3F7; padding:8px 0; z-index:1;`.
* Contains Previous/Next buttons and circular page buttons (32px) with active page background `#2196f3`.
* Disabled buttons at edges show reduced opacity.
* Pagination calculated from `filteredData.length / itemsPerPage` (default 10).

---

## Invoice Modal (PDF)

* Triggered by clicking PDF icon on a card.
* Modal: centered fixed dialog `width:250px` on mobile, white background, border-radius `8px`, padding `24px`, box-shadow `0 8px 24px rgba(0,0,0,0.2)` with backdrop overlay.
* Modal captures `jobCardId` and `deliveryDate` from clicked card and stores in state.
* Modal contents:

  * Title: **Select Invoice Date** (font-size `18px`, font-weight `500`).
  * Dropdown **Invoice Date** with three options: `Current Date`, `Delivery Date`, `Pick a Date`.
  * Helper text: **"Select a date for the invoice"** (font-size `11px`).
  * If `Pick a Date` selected, show native datepicker input (styled, value in `YYYY-MM-DD`).
  * Submit button (full width, blue `#1976d2`) validates selection; on success format date per config and navigate to `/app/management/vehicle/jobcard/invoice/${jobCardId}`, passing `{invoiceDate, jobOrderId}` via `history.pushState` or query params.
* Modal can be closed by backdrop click, Escape key, or Close button. When open, body scroll locked.

---

## Data & Storage

* Load job history from `localStorage` key `jobHistory`, filter by `vehicleId` if provided.
* Dates stored in `YYYY-MM-DD` format.
* Config fallbacks:

  * `config.globalisation.dateFormat` or `DD-MM-YYYY`
  * `config.companyInfo.currencyCode` or `AED`
  * `config.globalisation.numberFormat.code` or `en-US`

---

## Formatting & Utilities

* Currency formatting via `Intl.NumberFormat` using currency code.
* Hours formatting: convert decimal hours to `HH:MM` and vice versa.
* Dates formatted per config or fallback.

---

## Filtering & Pagination Logic

* Filter flow: apply searchQuery against formatted dates/amounts and apply date filters (exact match) if provided.
* Compute `totalPages = Math.ceil(filteredData.length / itemsPerPage)`.
* Paginate results and render current page slice.

---

## Accessibility & UX

* Tooltips for icon buttons.
* Keyboard support: Escape closes modal; focus management for modal.
* Toast notifications for validation and errors (top-center, auto-dismiss 3s).
* Scroll lock when filter dialog or modal open.

---

## Implementation Notes

* All `localStorage` operations wrapped in `try/catch` with toast errors on failure.
* Use `DOMContentLoaded` to initialize state and render UI.
* Console.log major user actions for debugging (open modal, select date, navigate to invoice, filter, paginate).

---

## Output

Produce a **single self-contained HTML file** with inline CSS and JS implementing the Mobile Job History View per the spec above.

## Sample data
```js
[
  {
    "jobCardId": "JC-1001",
    "vehicleId": "VH-001",
    "arrivalDate": "2025-01-05",
    "deliveryDate": "2025-01-07",
    "totalHours": "04:30",
    "totalAmount": 820.50
  },
  {
    "jobCardId": "JC-1002",
    "vehicleId": "VH-001",
    "arrivalDate": "2025-02-10",
    "deliveryDate": "2025-02-11",
    "totalHours": "02:15",
    "totalAmount": 460.00
  },
  {
    "jobCardId": "JC-1003",
    "vehicleId": "VH-001",
    "arrivalDate": "2025-03-01",
    "deliveryDate": "2025-03-03",
    "totalHours": "06:45",
    "totalAmount": 1250.00
  },
  {
    "jobCardId": "JC-1004",
    "vehicleId": "VH-002",
    "arrivalDate": "2025-03-15",
    "deliveryDate": "2025-03-16",
    "totalHours": "03:30",
    "totalAmount": 575.20
  },
  {
    "jobCardId": "JC-1005",
    "vehicleId": "VH-003",
    "arrivalDate": "2025-04-02",
    "deliveryDate": "2025-04-04",
    "totalHours": "05:10",
    "totalAmount": 980.75
  },
  {
    "jobCardId": "JC-1006",
    "vehicleId": "VH-003",
    "arrivalDate": "2025-04-25",
    "deliveryDate": "2025-04-26",
    "totalHours": "01:45",
    "totalAmount": 300.00
  }
]
```

---
## Image
<img src='./assets/Screenshot 2025-11-20 132131.png'>
<img src='./assets/Screenshot 2025-11-20 132146.png'>