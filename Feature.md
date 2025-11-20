# Spare Parts — Mobile Card View (README)

## Goal

Create a **single self-contained HTML/CSS/JavaScript** page (or component) that switches to a **card-based mobile view** when the viewport width is **768px or below**. The data is stored in `localStorage` under the key `spareParts` and the mobile view must read from that same dataset.

This README describes the visual layout, interactions, responsive behavior, storage keys, and includes **mock data** you can drop directly into your page’s `<script>` block.

Reference image (uploaded):

```
/mnt/data/1553f955-955f-4642-91f4-74dc45e7f61e.png
```

---

## Mobile Layout (≤ 768px)

1. **Header**

   * Back arrow (top-left) and page title (e.g., **Spare Parts**) centered vertically.

2. **Toolbar (horizontal)**

   * Full-width **search input** with a search icon inside on the left (occupies most of width).
   * Two icon-only buttons on the right:

     * **Filter** (filter icon)
     * **Add** (+ icon)
   * Search filters cards in real-time by part name, part code, and description.

3. **Cards List**

   * Cards stacked vertically with **16px gap**.
   * Card style:

     * Background: **#FFFFFF**
     * Border-radius: **8px**
     * Padding: **16px**
     * Box-shadow: subtle (e.g., `0 2px 6px rgba(0,0,0,0.08)`)
   * Card content layout:

     * **Top row:** Part name (bold, larger) left; blue Edit icon button right.
     * **Code:** `Code: {partNumber}` in gray text under the top row.
     * **Status pill:** Active (green) / Inactive (red).
     * **Details section:** grid or stacked lines for:

       * Description:
       * Price:
       * Quantity:
       * Seller:
       * Expiry Date:
     * Each label is bold and values are normal weight.

4. **Empty state**

   * If there are no cards (empty dataset or no search results):

     * Centered message: **"No records found"**
     * Subtitle: *"Try adjusting your search or filter criteria"* (gray text)

5. **Fixed Pagination Bar (bottom)**

   * Fixed to the bottom of viewport, background `#F1F3F7`.
   * Contains: Previous arrow, page numbers (clickable, current page highlighted blue), Next arrow.
   * The main content area must have additional bottom padding so the last card isn't hidden by the fixed bar.

6. **Filter Panel (mobile)**

   * Triggered by the Filter icon — slides in from right or appears as an overlay (width ~320px).
   * Panel header: **FILTERS** (left), a blue **RESET** text button (middle), and an **X** close icon (right).
   * Contains a **Seller Name** dropdown with all supplier options. (Selecting a filter closes the panel and applies filter.)
   * When the panel is open, add a CSS class to the `body` (e.g., `.no-scroll`) to disable background scrolling (`overflow: hidden`).

7. **Loading State**

   * Show an animated spinner centered in the content while data loads (simulate with a short timeout if needed).

---

## Behavior & Interactions

* The page should detect viewport width via CSS media queries and (optionally) JavaScript `matchMedia` to switch layout.
* On page load, read `spareParts` from `localStorage` (if missing, populate with the provided mock data) and render cards.
* **Search**: realtime filter across `name`, `partNumber`, and `description` as the user types. Reset pagination to page 1 on change.
* **Filter**: selecting Seller filter closes the panel, filters list, resets pagination to page 1.
* **Add**: The Add button can open an add-part modal or navigate to an Add page — implement a placeholder action (e.g., alert or modal).
* **Edit**: Edit icon on card triggers an edit action — implement a placeholder (e.g., navigate to an edit page or open an edit modal).
* **Pagination**: Implement client-side pagination for the filtered results.
* **No-scroll**: When filter panel is open, add `body.no-scroll { overflow: hidden; }`.

---

## Responsive Rules

* Hide any desktop table UI on mobile (use `display: none` in media queries) and render card view.
* Cards occupy full width minus page padding (e.g., `padding: 16px` on container).
* Ensure the bottom fixed pagination bar doesn't overlap final card content by adding bottom padding equal to the bar height.

---

## Storage

* **Key:** `spareParts`
* Read on load; write when creating/updating/deleting parts.
* Use `JSON.parse()` / `JSON.stringify()` with `try/catch`.

---

## Mock Data (sample `spareParts` array)

Drop this into your `<script>` if `localStorage.spareParts` is empty — it contains 20 sample entries:

```js
const sampleSpareParts = [
  { id: 'SP001', name: 'Brake Pad', partNumber: 'BP-1001', description: 'Front brake pad set', price: 120.5, quantity: 25, supplier: 'Supplier A', expiry: '2026-12-31', status: 'Active' },
  { id: 'SP002', name: 'Oil Filter', partNumber: 'OF-2002', description: 'High-flow oil filter', price: 45.0, quantity: 100, supplier: 'Supplier B', expiry: '2027-03-15', status: 'Active' },
  { id: 'SP003', name: 'Air Filter', partNumber: 'AF-3003', description: 'Cabin air filter', price: 35.75, quantity: 60, supplier: 'Supplier C', expiry: '2027-01-20', status: 'Inactive' },
  { id: 'SP004', name: 'Battery - 12V', partNumber: 'BAT-4004', description: '12V lead-acid battery', price: 220.0, quantity: 12, supplier: 'Supplier D', expiry: '2028-05-10', status: 'Active' },
  { id: 'SP005', name: 'Headlight Bulb', partNumber: 'HB-5005', description: 'Halogen headlight bulb', price: 18.25, quantity: 200, supplier: 'Supplier E', expiry: '2029-11-11', status: 'Active' },
  { id: 'SP006', name: 'Spark Plug', partNumber: 'SPG-6006', description: 'Iridium spark plug', price: 12.0, quantity: 500, supplier: 'Supplier F', expiry: '2030-07-01', status: 'Active' },
  { id: 'SP007', name: 'Fuel Pump', partNumber: 'FP-7007', description: 'Electric fuel pump', price: 185.0, quantity: 8, supplier: 'Supplier G', expiry: '2026-09-09', status: 'Inactive' },
  { id: 'SP008', name: 'Timing Belt', partNumber: 'TB-8008', description: 'Timing belt kit', price: 95.0, quantity: 30, supplier: 'Supplier H', expiry: '2028-04-04', status: 'Active' },
  { id: 'SP009', name: 'Alternator', partNumber: 'ALT-9009', description: 'Alternator assembly', price: 320.0, quantity: 6, supplier: 'Supplier I', expiry: '2029-02-14', status: 'Active' },
  { id: 'SP010', name: 'Radiator Hose', partNumber: 'RH-1010', description: 'Upper radiator hose', price: 25.5, quantity: 75, supplier: 'Supplier J', expiry: '2026-10-30', status: 'Active' },
  { id: 'SP011', name: 'Wheel Bearing', partNumber: 'WB-1111', description: 'Front wheel bearing', price: 48.0, quantity: 40, supplier: 'Supplier K', expiry: '2027-12-12', status: 'Active' },
  { id: 'SP012', name: 'Clutch Plate', partNumber: 'CP-1212', description: 'Clutch plate assembly', price: 260.0, quantity: 5, supplier: 'Supplier L', expiry: '2028-08-18', status: 'Inactive' },
  { id: 'SP013', name: 'Brake Disc', partNumber: 'BD-1313', description: 'Front brake disc', price: 85.0, quantity: 22, supplier: 'Supplier M', expiry: '2029-06-06', status: 'Active' },
  { id: 'SP014', name: 'AC Compressor', partNumber: 'AC-1414', description: 'Air conditioning compressor', price: 450.0, quantity: 4, supplier: 'Supplier N', expiry: '2030-01-01', status: 'Active' },
  { id: 'SP015', name: 'Fuel Filter', partNumber: 'FF-1515', description: 'Inline fuel filter', price: 22.0, quantity: 120, supplier: 'Supplier O', expiry: '2026-07-07', status: 'Active' },
  { id: 'SP016', name: 'Brake Fluid', partNumber: 'BF-1616', description: 'DOT4 brake fluid 1L', price: 9.5, quantity: 300, supplier: 'Supplier P', expiry: '2025-12-31', status: 'Active' },
  { id: 'SP017', name: 'Power Steering Fluid', partNumber: 'PSF-1717', description: 'Power steering fluid 1L', price: 11.75, quantity: 80, supplier: 'Supplier Q', expiry: '2026-03-03', status: 'Inactive' },
  { id: 'SP018', name: 'Serpentine Belt', partNumber: 'SB-1818', description: 'Serpentine belt', price: 40.0, quantity: 60, supplier: 'Supplier R', expiry: '2028-09-09', status: 'Active' },
  { id: 'SP019', name: 'Head Gasket', partNumber: 'HG-1919', description: 'Cylinder head gasket', price: 150.0, quantity: 10, supplier: 'Supplier S', expiry: '2029-04-04', status: 'Active' },
  { id: 'SP020', name: 'Oil Drain Plug', partNumber: 'ODP-2020', description: 'Magnetic oil drain plug', price: 6.25, quantity: 400, supplier: 'Supplier T', expiry: '2031-01-01', status: 'Active' }
];

// Save to localStorage if empty
try {
  if (!localStorage.getItem('spareParts')) {
    localStorage.setItem('spareParts', JSON.stringify(sampleSpareParts));
  }
} catch (e) {
  console.error('Failed to initialize spareParts in localStorage', e);
}
```

---

## Implementation Notes

* Use CSS `@media` queries for `max-width: 768px` to hide desktop table markup and show the mobile card layout.
* Optionally use `window.matchMedia('(max-width: 768px)')` in JS to toggle behaviors or attach different event listeners.
* Remember to add bottom padding to the main content container equal to the pagination bar height.
* Debounce search input for performance on large datasets.
* All writes to localStorage should use `try/catch` and provide user feedback (toasts) on failure.

---

## Accessibility

* Ensure buttons and inputs are reachable via keyboard.
* Provide `aria-label` attributes for icon-only buttons (Filter, Add, Back).
* Use proper semantic HTML (`<header>`, `<main>`, `<nav>`, `<ul>` for cards if desired).

---

## Output

Produce a single self-contained HTML file (with inline CSS/JS) implementing the card-based mobile view that reads and writes to `localStorage.spareParts`. The page should:

* Render mock data if localStorage is empty
* Support real-time search, seller filter panel, pagination, add/edit placeholders, and proper responsive behavior

---

## Image
<img src='./assets/Screenshot 2025-11-20 123735.png'>
<img src='./assets/Screenshot 2025-11-20 123756.png'>
<img src='./assets/Screenshot 2025-11-20 123807.png'>