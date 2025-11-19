# Employee Management List — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) designed for desktop (1024px and above) that implements an **Employee Management List** UI. The page should be clean and modern with a purple-accent theme and must be fully interactive using vanilla JavaScript.

The page should include a white card-style table centered on a light-gray background and provide search, filters, pagination, export/add buttons, row actions (Edit/Delete), and accessible tooltips.

---

## Page location

This page should be available at:

```
http://127.0.0.1:5500/operations/employee-management.html
```

The Add button navigates to:

```
http://127.0.0.1:5500/operations/employee-management/add.html
```

Edit button navigates to:

```
http://127.0.0.1:5500/operations/employee-management/edit/{employeeId}.html
```

---

## Visual & Layout Requirements

* Desktop-targeted layout (1024px+).
* Background: light gray.
* Centered white card-style table with:

  * Rounded corners: **15px**
  * Subtle shadow
  * Table header with clear labels
* Row backgrounds alternate:

  * **Odd rows:** `#F7F6FE`
  * **Even rows:** `#FFFFFF`
* Table columns: **Name**, **Employee ID**, **Roles** (colored chips), **Primary Contact**, **Secondary Contact**, **Actions**.
* Actions column: two icons per row:

  * **Edit** icon — blue; tooltip: "Edit"; clicking navigates to edit page.
  * **Delete** icon — red; tooltip: "Delete"; clicking asks for confirmation and on Yes shows a success message.
* All interactive elements show a dark tooltip with white text on hover.
* Use **Helvetica** font (or fallbacks).

---

## Roles Chip Colors

* Technician — **blue**
* Supervisor — **green**
* Manager — **purple**
* Advisor — **orange**

Chips should have rounded pill styling, small padding, and readable contrast.

---

## Toolbar (Above the Table)

* Left side: **Search bar** with placeholder: "Search employees..." — filters all table columns in real time (case-insensitive).
* Center/left: three dropdown filters:

  * **Employee Type:** All, Permanent, Contract, Temporary
  * **Roles:** All + role options (Technician, Supervisor, Manager, Advisor)
  * **Company:** All + `ABC Motors`, `XYZ Auto`, `Premium Cars`, `Elite Service`
* Filters work independently and in combination with the search.
* Right side: two icon buttons:

  * **Export** (download icon) — gray, turns blue on hover; clicking triggers a CSV download of currently visible rows and logs the action.
  * **Add** (plus icon) — gray, turns blue on hover; clicking navigates to the Add page and logs the action.

---

## Table Behavior & Interactions

* Rows are clickable for selection (highlight visually) — clicking a row logs the selected employee to console.
* Edit action: navigate to `.../edit/{employeeId}.html` and log the action.
* Delete action: show a confirmation dialog: "Are you sure you want to delete {employeeName}?" If Yes, remove the row from the table (and from the in-memory dataset), show a temporary success message "Employee {employeeName} deleted successfully.", and log the deletion. (No server calls — all client-side.)
* All UI actions (search, filters, page changes, button clicks, dialog results) should `console.log()` useful debug info.

---

## Pagination

* Pagination block centered under the table.
* Rows per page dropdown: **10, 20, 30, 40**.
* Page info display: e.g. "1–10 of X".
* Previous/Next buttons — disabled at edges (reduced opacity) and log actions.
* Clickable page numbers; current page highlighted in **blue** `#2196f3`.
* Show up to **5** page numbers; use ellipses `...` for longer ranges.
* All paging is calculated from the **filtered dataset**.

---

## Accessibility & Tooltips

* Tooltips: dark background with white text; appear on hover/focus of interactive icons.
* Keyboard accessible controls (tab navigation) for search, filters, buttons, and action icons.
* Provide `aria-label` on action buttons and table rows where appropriate.

---

## Sample Data (16 Employees)

Include this hardcoded dataset inside the page's `<script>` as the initial data source:

```js
const employees = [
  { name: 'Arjun Kumar', id: 'EMP001', role: 'Technician', type: 'Permanent', company: 'ABC Motors', primary: '+91-9876540001', secondary: '+91-9876500001' },
  { name: 'Bhavana R', id: 'EMP002', role: 'Supervisor', type: 'Permanent', company: 'XYZ Auto', primary: '+91-9876540002', secondary: '+91-9876500002' },
  { name: 'Chirag S', id: 'EMP003', role: 'Manager', type: 'Permanent', company: 'Premium Cars', primary: '+91-9876540003', secondary: '+91-9876500003' },
  { name: 'Deepa N', id: 'EMP004', role: 'Advisor', type: 'Contract', company: 'Elite Service', primary: '+91-9876540004', secondary: '+91-9876500004' },
  { name: 'Eshan P', id: 'EMP005', role: 'Technician', type: 'Temporary', company: 'ABC Motors', primary: '+91-9876540005', secondary: '+91-9876500005' },
  { name: 'Farah T', id: 'EMP006', role: 'Supervisor', type: 'Permanent', company: 'XYZ Auto', primary: '+91-9876540006', secondary: '+91-9876500006' },
  { name: 'Gautam R', id: 'EMP007', role: 'Technician', type: 'Permanent', company: 'Premium Cars', primary: '+91-9876540007', secondary: '+91-9876500007' },
  { name: 'Hema S', id: 'EMP008', role: 'Advisor', type: 'Contract', company: 'Elite Service', primary: '+91-9876540008', secondary: '+91-9876500008' },
  { name: 'Irfan K', id: 'EMP009', role: 'Manager', type: 'Permanent', company: 'ABC Motors', primary: '+91-9876540009', secondary: '+91-9876500009' },
  { name: 'Jaya M', id: 'EMP010', role: 'Technician', type: 'Permanent', company: 'XYZ Auto', primary: '+91-9876540010', secondary: '+91-9876500010' },
  { name: 'Karan V', id: 'EMP011', role: 'Supervisor', type: 'Temporary', company: 'Premium Cars', primary: '+91-9876540011', secondary: '+91-9876500011' },
  { name: 'Laila Z', id: 'EMP012', role: 'Technician', type: 'Permanent', company: 'Elite Service', primary: '+91-9876540012', secondary: '+91-9876500012' },
  { name: 'Manoj P', id: 'EMP013', role: 'Advisor', type: 'Permanent', company: 'ABC Motors', primary: '+91-9876540013', secondary: '+91-9876500013' },
  { name: 'Nita R', id: 'EMP014', role: 'Manager', type: 'Contract', company: 'XYZ Auto', primary: '+91-9876540014', secondary: '+91-9876500014' },
  { name: 'Omar S', id: 'EMP015', role: 'Technician', type: 'Permanent', company: 'Premium Cars', primary: '+91-9876540015', secondary: '+91-9876500015' },
  { name: 'Priya K', id: 'EMP016', role: 'Supervisor', type: 'Permanent', company: 'Elite Service', primary: '+91-9876540016', secondary: '+91-9876500016' }
];
```

---

## Export Behavior

* The Export button should produce a CSV file of the currently visible (filtered/paged) rows and trigger a download. Log the CSV payload and filename to the console.

---

## Deletion Behavior

* Confirm deletion via modal/confirm dialog.
* On Yes: remove from dataset, re-render table, log action, and show a non-blocking success message.

---

## Debug Logging

* All user interactions must `console.log()` helpful messages for debugging (e.g., `Search: "..."`, `Filter: {role: 'Technician'}`, `Page: 2`, `Exported CSV rows: 10`, `Deleted: EMP005 - Eshan P`).

---

## Reference Image

If you want to include the project reference image in the README or implementation, use the uploaded asset path:

```
/mnt/data/1553f955-955f-4642-91f4-74dc45e7f61e.png
```

---

## Output

Produce a single self-contained HTML file with inline CSS and JavaScript implementing the UI and behaviors described. Would you like me to generate the full working HTML file now?

# Image
<img src='./assets/Screenshot 2025-11-19 140925.png'>
<img src='./assets/Screenshot 2025-11-19 140950.png'>
<img src='./assets/Screenshot 2025-11-19 141019.png'>