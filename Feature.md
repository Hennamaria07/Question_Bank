# Vehicle Management List

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) for a **Vehicle Management List** page designed for desktop (≥1024px). The page should display a white rounded card-style table centered on a light-gray background and include search, filters, brand autocomplete, export, actions, row expansion for job-card details, pagination, responsive behavior, and loading state.

Target URL for the page:

```
http://127.0.0.1:5500/app/management/vehicle/list.html
```

---

## UI & Layout

* Page background: light gray; table card: white with rounded corners (15px) and subtle shadow.
* Use **Helvetica** font.
* Table rows alternate background colors:

  * Odd rows: `#F7F6FE`
  * Even rows: `#FFFFFF`
* Rows are clickable to expand/collapse an accordion panel beneath the row showing job-card details in a 4-column grid (Date Arrived, Advisor, Est. Date of Delivery, Status) on a `#F5F5F5` background; if no job card exists show "No active job card".
* Expansion uses smooth collapse/expand animations. Clicking action icons must **not** trigger row expand/collapse (use `stopPropagation`).
* Status column shows a 25px colored dot with tooltip text (e.g., "In-progress", "Completed"); dot turns **red** if the estimated delivery date/time has passed and the status is not `Completed`, `Ready`, or `On Hold`.
* Loading spinner: centered 100px rotating spinner while fetching data (simulate a short delay).

---

## Toolbar

* Left: **Search bar** that filters all columns in real time (plate, brand, VIN, owner, contact).
* Brand: **autocomplete** dropdown (50+ brands, alphabetically sorted) with search icon; selecting brand filters the table.
* Status: dropdown filter to filter by vehicle status.
* Right: **Export** button that saves current filtered results to an Excel file named `vehicle_data.xlsx` with specified formatting (bold centered headers, wrapped text, column width 27) — log the export action in console.
* Add button: navigates to `http://127.0.0.1:5500/app/management/vehicle/add/{userId}.html` (show alert simulating navigation) and log action.

---

## Columns & Behavior

Columns to show:

1. Plate No.
2. Brand (with searchable autocomplete)
3. VIN
4. Owner (first + last name)
5. Contact (hidden on tablets <1200px)
6. Status (colored dot with tooltip)
7. Actions: Job Card (wrench), Edit (blue), Delete (red), History (clock), QR Code — QR shows alert: `QR Code generation clicked for {plateNumber}`.

* Rows alternate colors and are clickable to expand an accordion panel showing job-card details (or “No active job card”).
* Action icons produce alerts or navigations:

  * Job Card → `http://127.0.0.1:5500/app/management/vehicle/jobcard/{vehicleId}.html`
  * Edit → `http://127.0.0.1:5500/app/management/vehicle/edit/{vehicleId}.html`
  * Delete → confirmation, then navigate to `http://127.0.0.1:5500/app/management/vehicle/delete/{vehicleId}.html` (simulate and log).
  * History → `http://127.0.0.1:5500/app/management/vehicle/jobcard/history/{vehicleId}.html`
  * QR Code → alert as above.
* Ensure action button clicks do **not** expand/collapse rows (use `event.stopPropagation()`).

---

## Status Logic

* Status dot colors map to statuses (for example):

  * `In-progress` → blue
  * `Completed` → green
  * `Ready` → teal
  * `On Hold` → gray
  * `Pending` → orange
* For any vehicle where `estimatedDelivery` date/time is **in the past** and the status is **not** `Completed`, `Ready`, or `On Hold`, render the status dot **red** to indicate overdue.

---

## Row Details Panel

* Expands/collapses under the row with smooth animation.
* Shows job-card details in a 4-column grid:

  * Date Arrived
  * Advisor
  * Estimated Date of Delivery (date + time)
  * Status
* If no active job card: display centered text "No active job card".

---

## Sample Data (20 Vehicles)

Include the following hardcoded array inside the page's `<script>` as the initial dataset. Each object includes `id`, `plate`, `brand`, `vin`, `owner`, `contact`, `status`, and `jobCard` (nullable or object):

```js
const vehicles = [
  { id: 'V001', plate: 'ABC-1234', brand: 'Toyota Camry', vin: '1HGBH41JXMN109186', owner: 'John Smith', contact: '+971-501234567', status: 'In-progress', estimatedDelivery: '2025-11-19T11:30:00', jobCard: { dateArrived: '2025-11-18', advisor: 'Anees', estDelivery: '2025-11-19T11:30:00', status: 'In-progress' } },
  { id: 'V002', plate: 'DEF-5678', brand: 'Honda Civic', vin: '2HGBH41JXMN109187', owner: 'Maria Lopez', contact: '+971-502345678', status: 'Completed', estimatedDelivery: '2025-11-10T09:00:00', jobCard: { dateArrived: '2025-11-09', advisor: 'Ramesh', estDelivery: '2025-11-10T09:00:00', status: 'Completed' } },
  { id: 'V003', plate: 'GHI-9012', brand: 'Ford Fiesta', vin: '3HGBH41JXMN109188', owner: 'Ahmed Khan', contact: '+971-503456789', status: 'Pending', estimatedDelivery: '2025-11-15T14:00:00', jobCard: null },
  { id: 'V004', plate: 'JKL-3456', brand: 'BMW 3 Series', vin: '4HGBH41JXMN109189', owner: 'Sara Ali', contact: '+971-504567890', status: 'On Hold', estimatedDelivery: '2025-11-20T10:00:00', jobCard: { dateArrived: '2025-11-19', advisor: 'Kiran', estDelivery: '2025-11-20T10:00:00', status: 'On Hold' } },
  { id: 'V005', plate: 'MNO-7890', brand: 'Mercedes C-Class', vin: '5HGBH41JXMN109190', owner: 'Peter Brown', contact: '+971-505678901', status: 'In-progress', estimatedDelivery: '2025-11-16T16:00:00', jobCard: { dateArrived: '2025-11-14', advisor: 'Joseph', estDelivery: '2025-11-16T16:00:00', status: 'In-progress' } },
  { id: 'V006', plate: 'PQR-1122', brand: 'Audi A4', vin: '6HGBH41JXMN109191', owner: 'Linda White', contact: '+971-506789012', status: 'Ready', estimatedDelivery: '2025-11-12T12:00:00', jobCard: { dateArrived: '2025-11-11', advisor: 'Anees', estDelivery: '2025-11-12T12:00:00', status: 'Ready' } },
  { id: 'V007', plate: 'STU-3344', brand: 'Hyundai Elantra', vin: '7HGBH41JXMN109192', owner: 'Mohammed Y', contact: '+971-507890123', status: 'In-progress', estimatedDelivery: '2025-11-10T08:00:00', jobCard: { dateArrived: '2025-11-09', advisor: 'Ramesh', estDelivery: '2025-11-10T08:00:00', status: 'In-progress' } },
  { id: 'V008', plate: 'VWX-5566', brand: 'Kia Sportage', vin: '8HGBH41JXMN109193', owner: 'Nina K', contact: '+971-508901234', status: 'Completed', estimatedDelivery: '2025-11-05T10:00:00', jobCard: { dateArrived: '2025-11-04', advisor: 'Kiran', estDelivery: '2025-11-05T10:00:00', status: 'Completed' } },
  { id: 'V009', plate: 'YZA-7788', brand: 'Ford Mustang', vin: '9HGBH41JXMN109194', owner: 'Carlos M', contact: '+971-509012345', status: 'Pending', estimatedDelivery: '2025-11-01T09:00:00', jobCard: null },
  { id: 'V010', plate: 'BCD-9900', brand: 'Toyota Corolla', vin: '0HGBH41JXMN109195', owner: 'Laila Z', contact: '+971-501111222', status: 'In-progress', estimatedDelivery: '2025-11-18T15:00:00', jobCard: { dateArrived: '2025-11-17', advisor: 'Joseph', estDelivery: '2025-11-18T15:00:00', status: 'In-progress' } },
  { id: 'V011', plate: 'EFG-1010', brand: 'Honda Accord', vin: '1HGBH41JXMN109196', owner: 'Rohit S', contact: '+971-501222333', status: 'In-progress', estimatedDelivery: '2025-10-30T10:00:00', jobCard: { dateArrived: '2025-10-28', advisor: 'Anees', estDelivery: '2025-10-30T10:00:00', status: 'In-progress' } },
  { id: 'V012', plate: 'HIJ-2020', brand: 'Nissan Altima', vin: '2HGBH41JXMN109197', owner: 'Zara H', contact: '+971-501333444', status: 'Ready', estimatedDelivery: '2025-11-02T11:00:00', jobCard: { dateArrived: '2025-11-01', advisor: 'Ramesh', estDelivery: '2025-11-02T11:00:00', status: 'Ready' } },
  { id: 'V013', plate: 'KLM-3030', brand: 'Chevrolet Malibu', vin: '3HGBH41JXMN109198', owner: 'Omar S', contact: '+971-501444555', status: 'Pending', estimatedDelivery: '2025-10-25T09:00:00', jobCard: null },
  { id: 'V014', plate: 'NOP-4040', brand: 'Volkswagen Golf', vin: '4HGBH41JXMN109199', owner: 'Priya K', contact: '+971-501555666', status: 'On Hold', estimatedDelivery: '2025-11-21T13:00:00', jobCard: { dateArrived: '2025-11-20', advisor: 'Kiran', estDelivery: '2025-11-21T13:00:00', status: 'On Hold' } },
  { id: 'V015', plate: 'QRS-5050', brand: 'Subaru Outback', vin: '5HGBH41JXMN109200', owner: 'Manoj P', contact: '+971-501666777', status: 'In-progress', estimatedDelivery: '2025-11-17T09:00:00', jobCard: { dateArrived: '2025-11-16', advisor: 'Joseph', estDelivery: '2025-11-17T09:00:00', status: 'In-progress' } },
  { id: 'V016', plate: 'TUV-6060', brand: 'Mazda 3', vin: '6HGBH41JXMN109201', owner: 'Alex G', contact: '+971-501777888', status: 'Completed', estimatedDelivery: '2025-11-03T14:00:00', jobCard: { dateArrived: '2025-11-02', advisor: 'Anees', estDelivery: '2025-11-03T14:00:00', status: 'Completed' } },
  { id: 'V017', plate: 'WXY-7070', brand: 'Tesla Model 3', vin: '7HGBH41JXMN109202', owner: 'Naveen K', contact: '+971-501888999', status: 'In-progress', estimatedDelivery: '2025-11-11T16:00:00', jobCard: { dateArrived: '2025-11-10', advisor: 'Ramesh', estDelivery: '2025-11-11T16:00:00', status: 'In-progress' } },
  { id: 'V018', plate: 'ZAB-8080', brand: 'Honda Jazz', vin: '8HGBH41JXMN109203', owner: 'Sana P', contact: '+971-501999000', status: 'Pending', estimatedDelivery: '2025-10-20T10:00:00', jobCard: null },
  { id: 'V019', plate: 'CDE-9090', brand: 'Toyota RAV4', vin: '9HGBH41JXMN109204', owner: 'Irfan K', contact: '+971-502000111', status: 'In-progress', estimatedDelivery: '2025-11-13T12:00:00', jobCard: { dateArrived: '2025-11-12', advisor: 'Kiran', estDelivery: '2025-11-13T12:00:00', status: 'In-progress' } },
  { id: 'V020', plate: 'FGH-1212', brand: 'BMW X5', vin: '0HGBH41JXMN109205', owner: 'Sohail R', contact: '+971-502111222', status: 'In-progress', estimatedDelivery: '2025-10-15T09:30:00', jobCard: { dateArrived: '2025-10-14', advisor: 'Joseph', estDelivery: '2025-10-15T09:30:00', status: 'In-progress' } }
];
```

> Note: some `estimatedDelivery` values are intentionally in the past to test overdue rendering.

---

## Pagination

* Rows per page options: **10, 20, 30, 40**.
* Page info: e.g., "1–10 of X".
* Previous/Next buttons (disabled at edges) and clickable page numbers.
* Simulate server-side paging by slicing the `vehicles` array for current page.

---

## Export to Excel

* Export current filtered results to an Excel file named `vehicle_data.xlsx`.
* Formatting requirements: bold centered headers, wrapped text, column width ~27.
* Log the export payload and filename to console.

---

## Brand Autocomplete

* Provide an autocomplete input with 50+ brand names (alphabetically sorted). Show a dropdown with matching brands as the user types and allow selection. Include a search icon inside the input.

---

## Responsive Behavior

* Hide **Contact** column on tablets (<1200px).
* Hide **Owner** column on narrower screens (780–880px).
* On tablets (780–1200px) adjust column widths to be approximately equal (min 100px, max 150px) and reduce visible columns to five.
* Ensure smooth transitions and readable typography on all viewports.

---

## Loading & UX

* Show a centered 100px rotating spinner while loading data (simulate short delay).
* Tooltips for status and action icons.
* All user actions should `console.log()` useful debug messages (search term, filter, export, add, pagination, delete, expand/collapse, etc.).

---

## Accessibility

* Tooltips accessible on hover and focus.
* Keyboard navigation for search, filters, pagination, and action buttons.

---

## Image
<img src='./assets/Screenshot 2025-11-19 143717.png'>
<img src='./assets/Screenshot 2025-11-19 143733.png'>
<img src='./assets/Screenshot 2025-11-19 143806.png'>
<img src='./assets/Screenshot 2025-11-19 143831.png'>
