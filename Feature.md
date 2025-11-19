# Services Management — README


Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) implementing a complete **Services Management Component**. The UI must follow a clean, purple-accent theme and remain fully responsive across desktop, mid-width, and mobile layouts.

---

## Header

* Display a clear top-left header: **Services**

  * Font size: **24px**
  * Font weight: **600 / bold**
  * Color: `#232323`

---

## Services Table — Overview

A responsive table listing all service rows with the following columns:

| Column          | Description                                                                                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Task**        | Async creatable dropdown populated from `serviceTypesData` (localStorage). Supports searching, filtering, and creating new service types when allowed. |
| **Description** | Auto-filled when a Task is selected. Read-only.                                                                                                        |
| **Est Hrs**     | Estimated hours (decimal). Read-only, pre-filled from selected service type.                                                                           |
| **Est Amt**     | Estimated amount (currency). Read-only, formatted with two decimals.                                                                                   |
| **RT Hrs**      | Regular Time hours, computed from timesheets. Read-only.                                                                                               |
| **OT Hrs**      | Overtime hours, computed. Read-only.                                                                                                                   |
| **Act Hrs**     | Total Actual Hours. Read-only.                                                                                                                         |
| **Act Amt**     | Editable actual amount. Validates two decimals and formats on blur.                                                                                    |
| **Action**      | Delete icon. May be disabled if restrictions apply.                                                                                                    |

---

## Task Selector (Async Creatable Dropdown)

* Loads **service types** from `localStorage` key: `serviceTypesData`.
* Must support:

  * Typing to filter options asynchronously.
  * Excluding already-selected service types.
  * Displaying **“No services found”** when empty.
  * Allowing creation of new service types.
  * Triggering the **Create New Service Modal** when user clicks *Create new service: 'X'*.

---

## Create New Service Modal

A modal (max width 600px) containing:

* **Service Name** (required)
* **Description** (required)
* **Estimated Hours**

  * Accept **hours + minutes**
  * Convert to decimal internally
* **Estimated Amount** (required, currency)

### Modal Behavior

* Validate all fields.
* Save the new service to `localStorage` → key: `serviceTypesData`.
* Add the new service to the dropdown list.
* Auto-select this new service in the row that created it.
* Show success/error toasts.

---

## Row Behavior

Each service row is represented internally as:

```js
{
  serviceType: '',
  serviceDescription: '',
  serviceApproxHrs: 0,
  serviceApproxCost: 0,
  serviceActualCost: 0,
  serviceActualHrs: 0,
  isNewService: false,
  hasUserChanged: false,
  modifiedFields: []
}
```

### When user selects a Task:

* Auto-fill:

  * Description
  * Estimated Hours (decimal)
  * Estimated Amount (currency)

### When user edits Actual Amount:

* Validate up to **two decimals**
* Reformat using `Intl.NumberFormat` on blur

### RT/OT/Actual Hours

* Compute using timesheet data from:

  * `timesheetsData_{jobCardId}`
* Ignore timesheets where `currentStatus === "REJECTED"`.

### Add/Delete Rows

* **Add Row** — Clicking the **+** icon (only shown on last row). Adds an empty row.
* **Delete Row** — Clicking Delete icon (trash).

  * Block deletion if:
    * Any actual hours > 0
  * Blocked delete shows tooltip explaining why.
  * Otherwise show confirmation dialog.

---

## Totals Section

At the bottom of the table, show readonly totals:

* Total **Estimated Hours**
* Total **RT Hours**
* Total **OT Hours**
* Total **Actual Hours**
* Total **Actual Amount** (formatted currency)

Totals update **live** whenever the services array changes.

---

## Autosave (Important)

All edits must update an autosave object in localStorage:

```
autoSaveJobOrder_{vehicleId}_{userId}
```

Autosave must:

* Use debounced updates
* Include create/edit/delete logic
* Log actions to console for debugging
* Use try/catch and show toast errors when failing

---

## Initialization Logic

When component loads:

1. Show a **centered spinner** while loading.
2. Load:

   * `serviceTypesData`
   * `servicesData_{jobCardId}` (if edit mode)
   * `timesheetsData_{jobCardId}`
3. If no saved services exist → start with **one empty row**.
4. Detect Add vs Edit mode from URL.

---

## Responsive Layout

### Desktop (≥1024px)

* Full table header visible
* Traditional row layout

### Mid-width (770–1024px)

* Two-column grid layout for each row

### Mobile (<768px)

* Stack fields with **data-labels**
* Hide table header entirely
* Full-width rows

---

## Utility Functions

Include these helper functions:

* Convert decimal hours ↔ HH:MM
* Format currency via `Intl.NumberFormat`
* Calculate totals from service array
* Deep clone objects

---

## Toast System

* Success toast (green)
* Error toast (red)
* Auto-dismiss after 3 seconds
* Positioned at top-center

---

## Data Dependencies (LocalStorage)

### `serviceTypesData`

List of service types:

```js
[
  {
    id: "SVC001",
    name: "Oil Change",
    description: "Engine oil replacement",
    estHrs: 1.0,
    estAmt: 150.00
  },
  {
    id: "SVC002",
    name: "Break Change",
    description: "Break replacement",
    estHrs: 2.0,
    estAmt: 100.00
  }
]
```

### `servicesData_{jobCardId}`

Array of existing service entries.

### `timesheetsData_{jobCardId}`

Timesheet logs from mechanics/technicians.

### `activeSessionsData_{jobCardId}`

Used to block deletes.

### `autoSaveJobOrder_{vehicleId}_{userId}`

Autosave store.

---

## Output

Produce a **single self-contained HTML file** that includes:

* Header
* Responsive services table
* Task selector (async + creatable)
* New Service modal
* Row logic & totals logic
* Autosave logic
* Dynamic delete rules
* Toasts
* Styling (purple theme, clean UI)
---

## Image
<img src='./assets/Screenshot 2025-11-19 152335.png'>
<img src='./assets/Screenshot 2025-11-19 152357.png'>