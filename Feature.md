# Parts Management Page

## Overview

Build a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) that implements a responsive **Parts Management** page supporting both **Add** and **Edit** modes. The page should be desktop-first but responsive down to small screens, use a purple-accent clean design, and persist data via `localStorage`.

---

## High-level Features

1. Store selector (required) at top-left — searchable, 25% width on desktop, full width on mobile; white background, blue focus.
2. Responsive Parts Table with:

   * Pale header, rounded corners, alternating row colors.
   * Each row has:

     * Searchable/creatable **Part** dropdown (loads 50+ hardcoded parts and includes any `customParts` saved to `localStorage`).
     * Read-only **Description** field populated from part metadata.
     * Read-only **Supplier** field populated from part metadata (20+ suppliers in sample data).
     * **Quantity** input (min 1) that auto-calculates **Amount = unitPrice × quantity**.
     * **Amount** input (editable) that accepts two decimals, reformats on blur, and recalculates unitPrice when edited.
     * **Delete** button (red).
   * The last row shows an **Add** button (blue) to append a new empty row.
   * Table footer shows **Est Total** (read-only), formatted with `Intl.NumberFormat` (commas, two decimals, currency code from config fallback).
3. **Create New Part** modal (max-width 600px) with fields:

   * Part Name, Part Code, Description, Supplier (dropdown of 20+ suppliers), Price, Qty, Expiry Date.
   * Validate inputs, compute cost = price × qty, and save as a `customParts` entry in `localStorage`.
   * Auto-select the newly created part in the current row.
   * Show success/error toasts.
4. **Add vs Edit modes**

   * Detect mode via URL (`mode=add` or `mode=edit&jobCardId=...`).
   * In **Edit mode** show a centered loading spinner while fetching `jobCardParts` from `localStorage`.
   * Populate rows from saved `jobCardParts` or start with a single empty row if none.
   * Track deleted row IDs for processing while editing.
5. Row interactions and validations:

   * Selecting a part fills description, supplier, unitPrice and amount.
   * Changing quantity recalculates amount.
   * Editing amount recalculates unitPrice (validated to two decimals) and reformats on blur.
   * Deleting removes row or resets it if it’s the only row; in Edit mode record deleted IDs.
6. Save/Update and Cancel buttons:

   * Bottom-centered Save/Update and Cancel.
   * Validate rows (disallow saving when there are no parts or when required fields are missing).
   * On save: process `rowsToDelete`, update existing entries, or create new `jobCardParts` in `localStorage` with `createdAt`, `updatedAt`, `userId`, and `active` flags.
   * Show success toast and keep clear user feedback for create/update/delete.
7. Accessibility & UX:

   * Accessible modals, keyboard focus, and ARIA attributes.
   * Toast notifications top-center auto-dismiss.
   * Custom scrollbars and loading spinners provided.

---

## Data & localStorage Keys

* `parts` — initial hardcoded catalog (50+ parts). Each part object:

```js
{ id: 'PART001', name: 'Brake Pad', code: 'BP-001', description: 'Front brake pad', supplier: 'Supplier A', unitPrice: 120.50, currency: 'USD', expiry: '2026-12-31' }
```

* `suppliers` — list of 20+ supplier names/objects.
* `customParts` — array of user-created parts added via the Create New Part modal.
* `jobCardParts` — array/object mapping jobCardId to its saved parts (used in Edit mode). Each saved part includes `id` (local id), `partId` (reference to parts/customParts), `qty`, `unitPrice`, `amount`, `createdAt`, `updatedAt`, `userId`, `active`.
* `stores` — available stores for the top selector.

The README includes example sample datasets (50 parts, 20 suppliers) embedded in the implementation.

---

## UI Details and Behavior

### Parts Dropdown

* Loads both `parts` and `customParts` and supports typing to filter.
* If user types a name that does not match, an option `Create new part: '{input}'` appears — clicking it opens the Create New Part modal with the typed name pre-filled.

### Quantity & Amount Logic

* Quantity default = 1, min = 1.
* Amount default = `unitPrice * qty` and displays two decimals.
* When Amount is edited by the user:

  * Validate input (allow two decimals), on blur reformat to two decimals.
  * Recalculate `unitPrice = amount / qty` and store.
* Est Total is sum of row amounts and updates live when rows change.

### Create New Part Modal

* Validates required fields (name, code, price, qty, supplier).
* Shows computed cost and saves the part to `customParts`.
* Upon success, modal closes and new part is selected in the originating row.
* New part saved with `createdAt`, `createdBy` (userId), and `active=true`.

### Add/Edit Mode specifics

* **Add mode**: label/buttons say "Save Parts" and create new `jobCardParts` entry on save.
* **Edit mode**: label/buttons say "Update Parts"; on load, fetch `jobCardParts[jobCardId]` and populate rows. Track `rowsToDelete` and mark deleted rows by ID instead of immediate removal.

### Validation & Errors

* Disallow saving when no parts rows exist or when required fields (part selection, qty) are missing.
* Show toasts describing specific validation errors (e.g., "Please select a part in row 2", "Quantity must be at least 1").

---

## Responsiveness & Layout

* Desktop (≥1024px): full table view with header and columns.
* Below 1024px: hide table header and render each row as stacked blocks with `data-label` indicators for each cell.
* Between 770–1104px: render each row as a 2-column grid for compact layout.
* Below 480px: compress spacing and stack controls vertically for thumb access.

---

## Formatting & Localization

* Use `Intl.NumberFormat` for Est Total and Amount formatting (two decimals, thousand separators). Currency code can come from page config or fallback to `USD`.
* Dates formatted via `toLocaleDateString` with a config fallback.

---

## Feedback & Logging

* All actions log to the console for debugging (e.g. `Added part PART123 to row 2`, `Deleted row ID 45`, `Saved jobCardParts for JC1001`).
* Toasts appear top-center and auto-dismiss after 3s for success; errors remain until user fixes the issue or 5s for critical errors.

---

## Security & Edge Cases

* Robust JSON parse/stringify handling for `localStorage` reads/writes with try/catch.
* Graceful handling when stored data is missing or malformed: fall back to initial datasets and show warnings.
* Prevent XSS by sanitizing user-entered strings (e.g., part names) before insertion into the DOM.

---

## Sample data (included in implementation)

* **50+ parts** (various categories: brakes, filters, oils, batteries, lights, sensors, belts, hoses, etc.)
* **20+ suppliers** (Supplier A..T) and a sample `stores` list.
* The implementation will include these arrays pre-populated in the `<script>` section.

---

## Accessibility

* Modal focus trap and ESC to close.
* Keyboard accessible dropdowns and buttons.
* ARIA labels for dynamic elements and toast announcements.

---

## Output

Produce a single self-contained file `parts.html` with inline CSS and JS implementing the described behaviors and using `localStorage` for persistence.

Would you like me to generate the full single-file implementation now?

---

## Image
<img src='./assets/Screenshot 2025-11-19 145704.png'>