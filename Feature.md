# Manual Time Entry — Desktop Data Table Component (README)

## Project Goal

Create a **responsive desktop data table component** (HTML + inline CSS + inline JavaScript) to display service/job order records. The table should be a modern, purple-themed, single-page component intended to live at:

```
http://127.0.0.1:5500/dashboard/manual-time-entry.html
```

Only desktop users (screen width **> 600px**) should see the table; it must be hidden on mobile (≤ 600px) via CSS media queries.

---

## Functional Requirements

1. **Data**

   * Use **static hardcoded data** inside the page (no server calls).
   * At least **25 job order records**.
   * Each record must include the following fields:

     * `Plate No` (vehicle plate number)
     * `Brand` (e.g. Toyota, Honda, Ford, BMW, Mercedes)
     * `Job Card ID` (string/number)
     * `Est Delivery` (date in `DD-MMM-YYYY` format, e.g. `05-Jun-2025`)
     * `Advisor Name` (string)

2. **Table Layout & Style**

   * Display five columns: **Plate No**, **Brand**, **Job Card ID**, **Est Delivery**, **Advisor Name**.
   * Header row: bold, uppercase text.
   * No visible borders between cells; table should have **rounded corners (15px)**.
   * Alternating row background colors: **even rows** `#F7F6FE`, **odd rows** `#FFFFFF`.
   * Hover effect on rows to highlight (smooth transition).
   * Clean spacing and typography; component background `#F1F3F7`.
   * Purple theme accent color: `#2A00B2` for active states, buttons, and pagination.

3. **Visibility / Responsiveness**

   * Entire component is **hidden** on screens `≤ 600px` using CSS media queries.
   * On desktop (`> 600px`) the table is fully visible and responsive to container width.

4. **Search & Filters**

   * A **search bar** placed top-right of the table filters results in real-time as the user types.
   * The search must filter across **all fields** (plate no, brand, job card id, advisor name).
   * Two dropdown filters next to the search bar:

     * **Brand** filter: options = unique brands from the dataset + `All`.
     * **Advisor** filter: options = unique advisor names from the dataset + `All`.
   * Filters work independently and combinationally with the search input.
   * A **Reset Filters** button clears search input and sets both dropdowns to `All`.
   * Whenever search or filter values change, the table **resets to page 1**.

5. **Pagination**

   * Show **10 records per page**.
   * Include **Previous** and **Next** buttons and numbered page buttons for direct navigation.
   * Display text `Showing X to Y of Z entries` based on the (filtered) results.
   * Page count should be calculated from the **filtered dataset**.

6. **Row Interaction**

   * Each table row is **clickable**. Clicking a row simulates navigation to:

     * `http://127.0.0.1:5500/dashboard/manual-time-entry/manual-time-add.html`
   * Use a smooth cursor change (pointer) and click transition effect.

7. **Behavioral Details**

   * Searching, filtering, and pagination must work **together** (e.g., searching + brand filter + advisor filter updates the page count, the visible rows, and the `Showing X to Y of Z` text).
   * Changing search/filter resets the current page to the first page.
   * All operations should be instantaneous and client-side (no reloads or button clicks required for search).

---

## Implementation Guidance

* Deliver as a **single standalone HTML file** with inline CSS and JavaScript.
* Use semantic HTML (`<table>`, `<thead>`, `<tbody>`) for accessibility.
* Implement the dataset as a JavaScript array of objects within the page.
* Build the brand and advisor dropdown options dynamically from the dataset when the page loads.
* Implement the search as a case-insensitive substring match on all searchable fields.
* Use modern, vanilla JavaScript (ES6+); do not rely on external libraries.
* Ensure smooth transitions (CSS `transition`) for hover effects, pagination, and UI interactions.

---

## Image
<img src='./assets/Screenshot 2025-11-19 130432.png'>
<img src='./assets/Screenshot 2025-11-19 130543.png'>
<img src='./assets/Screenshot 2025-11-19 130609.png'>

## Hardcoded Dataset (25 Records)
You can directly paste this into your <script> section as:
```js
const jobOrders = [
  { plateNo: "KL-07-AB-1234", brand: "Toyota", jobCardId: "JC1001", estDelivery: "05-Jun-2025", advisor: "Anees" },
  { plateNo: "KL-08-CD-5678", brand: "Honda", jobCardId: "JC1002", estDelivery: "10-Jun-2025", advisor: "Ramesh" },
  { plateNo: "KL-10-EF-9012", brand: "Ford", jobCardId: "JC1003", estDelivery: "12-Jun-2025", advisor: "Kiran" },
  { plateNo: "KL-11-GH-3456", brand: "BMW", jobCardId: "JC1004", estDelivery: "15-Jun-2025", advisor: "Anees" },
  { plateNo: "KL-12-IJ-7890", brand: "Mercedes", jobCardId: "JC1005", estDelivery: "18-Jun-2025", advisor: "Ramesh" },

  { plateNo: "KL-13-KL-1122", brand: "Toyota", jobCardId: "JC1006", estDelivery: "20-Jun-2025", advisor: "Joseph" },
  { plateNo: "KL-14-MN-3344", brand: "Honda", jobCardId: "JC1007", estDelivery: "22-Jun-2025", advisor: "Kiran" },
  { plateNo: "KL-15-OP-5566", brand: "Ford", jobCardId: "JC1008", estDelivery: "25-Jun-2025", advisor: "Anees" },
  { plateNo: "KL-16-QR-7788", brand: "BMW", jobCardId: "JC1009", estDelivery: "28-Jun-2025", advisor: "Ramesh" },
  { plateNo: "KL-17-ST-9900", brand: "Mercedes", jobCardId: "JC1010", estDelivery: "30-Jun-2025", advisor: "Joseph" },

  { plateNo: "KL-18-UA-1111", brand: "Toyota", jobCardId: "JC1011", estDelivery: "02-Jul-2025", advisor: "Anees" },
  { plateNo: "KL-19-VB-2222", brand: "Honda", jobCardId: "JC1012", estDelivery: "05-Jul-2025", advisor: "Ramesh" },
  { plateNo: "KL-20-WC-3333", brand: "Ford", jobCardId: "JC1013", estDelivery: "07-Jul-2025", advisor: "Kiran" },
  { plateNo: "KL-21-XD-4444", brand: "BMW", jobCardId: "JC1014", estDelivery: "10-Jul-2025", advisor: "Joseph" },
  { plateNo: "KL-22-YE-5555", brand: "Mercedes", jobCardId: "JC1015", estDelivery: "12-Jul-2025", advisor: "Anees" },

  { plateNo: "KL-23-ZF-6666", brand: "Toyota", jobCardId: "JC1016", estDelivery: "15-Jul-2025", advisor: "Kiran" },
  { plateNo: "KL-24-AG-7777", brand: "Honda", jobCardId: "JC1017", estDelivery: "17-Jul-2025", advisor: "Ramesh" },
  { plateNo: "KL-25-BH-8888", brand: "Ford", jobCardId: "JC1018", estDelivery: "20-Jul-2025", advisor: "Joseph" },
  { plateNo: "KL-26-CI-9999", brand: "BMW", jobCardId: "JC1019", estDelivery: "22-Jul-2025", advisor: "Anees" },
  { plateNo: "KL-27-DJ-1010", brand: "Mercedes", jobCardId: "JC1020", estDelivery: "25-Jul-2025", advisor: "Kiran" },

  { plateNo: "KL-28-EK-2020", brand: "Toyota", jobCardId: "JC1021", estDelivery: "27-Jul-2025", advisor: "Joseph" },
  { plateNo: "KL-29-FL-3030", brand: "Honda", jobCardId: "JC1022", estDelivery: "30-Jul-2025", advisor: "Anees" },
  { plateNo: "KL-30-GM-4040", brand: "Ford", jobCardId: "JC1023", estDelivery: "01-Aug-2025", advisor: "Ramesh" },
  { plateNo: "KL-31-HN-5050", brand: "BMW", jobCardId: "JC1024", estDelivery: "03-Aug-2025", advisor: "Kiran" },
  { plateNo: "KL-32-IO-6060", brand: "Mercedes", jobCardId: "JC1025", estDelivery: "05-Aug-2025", advisor: "Joseph" },
];
```