# Suppliers Management — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + vanilla JavaScript) implementing a **Suppliers Management** page. The page stores and displays supplier records in `localStorage`, is easy to use, responsive, and visually consistent with a purple-accent theme.

This README describes the required UI, behavior, data format, and includes **mock data** to initialize `localStorage.suppliers` for testing.

---

## Page Path

**URL pattern:** `/app/settings/suppliers/{userId}.html`  
`userId` is read from the URL and used when constructing Add/Edit navigation links.

---

## Layout & Visuals

* Page background: `#F1F3F7`.
* Main container: card-like area with padding `16px`, background `#F1F3F7` (or slightly lighter white card inside), rounded corners, and subtle shadow.
* Purple theme accents (buttons, headings, highlights) — use `#2A00B2` (dark purple) for primary actions.

### Table styling
* Responsive data table inside a white card:
  * Header background: `#D0D4F2`
  * Header text: uppercase, bold
  * Rounded header corners
  * Row striping: odd → `#F7F6FE`, even → `#FFFFFF`
  * No visible grid borders; subtle cell padding and rounded corners on cells where appropriate
  * Table and cell typography: readable font-size, consistent padding
* On narrow screens:
  * Hide some address columns to keep layout readable
  * Table becomes horizontally scrollable when needed

---

## Columns

* **Supplier Name**
* **Supplier Id**
* **Address Line 1**
* **Address Line 2**
* **Contact Number**
* **Status** — badge: “Active” (green badge) or “Inactive” (red badge)
* **Actions** — Edit button (navigates to `/app/settings/suppliers/edit/{supplierId}.html`)

---

## Toolbar & Controls

* Top-right toolbar:
  * **Add** button — navigates to `/app/settings/suppliers/add/{userId}.html` (userId from URL)
* Search box (live):
  * Filters table as user types across `name`, `supplierId`, `addressLine1`, `addressLine2`, `contactNumber`
  * Resets pagination to page 1 when changed
* Column filters:
  * **Supplier Name** dropdown (populated from full list)
  * **Supplier Id** dropdown (populated from full list)
  * Clearing filters resets the view and page to 1
* Pagination controls:
  * Rows per page selector: 10 / 20 / 30 / 40
  * Previous / Next buttons
  * Page indicator and total count, e.g. `Showing 11–20 of 42 entries`
  * Pagination is simulated client-side by slicing the filtered array

---

## Behavior & Data Handling

* On load:
  * Show a centered loading spinner while reading data from `localStorage` (short delay allowed).
  * Ensure `localStorage.suppliers` exists; if not, initialize with the provided mock data (or an empty array depending on implementation choice).
  * Load both:
    * `fullSuppliers` — unpaginated complete list (used to populate filters)
    * `data` — paginated slice derived from the filtered set for display
* State variables to maintain:
  * `data` (display slice), `fullSuppliers`, `searchQuery`, `filters`, `page`, `rowsPerPage`, `totalCount`
* Searching, filtering, and changing rows-per-page reset `page` to 1 and re-render the display slice.
* Empty results should show a friendly message like:  
  `No records found / Try adjusting your search or filter criteria`
* All localStorage access must use `JSON.parse` / `JSON.stringify` inside `try/catch` with graceful fallbacks to prevent UI crashes.

---

## Validation rules (for Add/Edit pages)

* When adding or editing suppliers (this page displays and navigates to add/edit pages):
  * `supplierId` must be unique across `localStorage.suppliers`. Adding/editing code should check uniqueness before saving.

---

## Visual & Interaction Details

* Active badge:
  * Green text/icon on a light-green background (or green pill)
  * Ensure color contrast is accessible
* Inactive badge:
  * Red text/icon on a light-red background
* Action buttons:
  * Tooltips on hover
  * Hover transitions (opacity, slight scale) with `0.15s–0.2s` transitions
* Focus states:
  * Inputs, buttons should show visible focus outlines for accessibility

---

## Implementation Requirements

* Use **plain DOM APIs** only:
  `createElement`, `appendChild`, `querySelector`, `addEventListener`, etc.
* Keep logic readable:
  * Modular functions for loading localStorage, rendering filters, applying search/filter, paginating, rendering rows, and saving data
* All operations must update localStorage (when applicable) and the UI immediately (no external server)
* Provide clear comments in code to explain non-trivial logic

---

## Mock Data (initialize localStorage.suppliers)

Place this snippet into your JS initialization logic (or run in the console) if `localStorage.suppliers` is missing — it provides test data to exercise the UI:

```js
// Initialize mock data if none exists
[
      {
        _id: "1",
        name: "Alpha Traders",
        supplierId: "SUP001A1",
        contactNumber: "+971501234567",
        addressLine1: "Business Bay",
        addressLine2: "Office 101",
        active: true,
        userId: "user123"
      },
      {
        _id: "2",
        name: "Beta Supplies",
        supplierId: "SUP002B2",
        contactNumber: "+971502345678",
        addressLine1: "Deira Market",
        addressLine2: "Warehouse 5",
        active: false,
        userId: "user123"
      },
      {
        _id: "3",
        name: "Gamma Corporation",
        supplierId: "SUP003C3",
        contactNumber: "+971503456789",
        addressLine1: "Jumeirah",
        addressLine2: "Suite 10",
        active: true,
        userId: "user123"
      },
      {
        _id: "4",
        name: "Delta Wholesale",
        supplierId: "SUP004D4",
        contactNumber: "+971504567890",
        addressLine1: "Al Quoz",
        addressLine2: "",
        active: true,
        userId: "user456"
      },
      {
        _id: "5",
        name: "Epsilon Parts",
        supplierId: "SUP005E5",
        contactNumber: "+971505678901",
        addressLine1: "Sharjah Industrial Area",
        addressLine2: "Block B",
        active: false,
        userId: "user123"
      }
    ]
```

---
## Image
<img src='./assets/Screenshot 2025-11-20 112635.png'>
<img src='./assets/Screenshot 2025-11-20 112654.png'>
<img src='./assets/Screenshot 2025-11-20 112735.png'>