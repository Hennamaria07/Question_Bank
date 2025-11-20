# Mobile Employee Management List 
## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) optimized for **mobile screens (≤ 600px)** that implements an **Employee Management List** UI. The page displays employee cards, supports search, filtering, pagination, and basic actions (Edit/Delete), and uses `localStorage` for the data source.

---

## Visual Style & Layout

* Page background: `#F1F3F7`, side padding `16px`, extra top/bottom padding `80px` to account for fixed controls and pagination.
* Cards: white background, `border-radius: 8px`, `padding: 16px`, `margin-bottom: 16px`, `box-shadow: 0 2px 4px rgba(0,0,0,0.1)`.
* Fonts: `Helvetica, "Helvetica Neue", Arial, sans-serif`.
* Touch-friendly controls with minimum 40px tap targets and smooth `transition: 0.2s` on interactive elements.

---

## Card Design (per employee)

Each card displays:

* **Name** — bold, 18px.
* **Employee ID** — prefixed `ID: `, 13px gray.
* **Role chip** — colored pill with 0.1 opacity background and colored text:

  * Technician — `#5B8FF9`
  * Supervisor — `#52C41A`
  * Manager — `#722ED1`
  * Advisor — `#FA8C16`
  * Chip style: `padding: 4px 12px; border-radius: 12px; font-size: 13px; display: inline-block;`
* **Employee Type** — prefixed `Type: ` (bold)
* **Company** — prefixed `Company: ` (bold)
* **Primary Contact** — prefixed `Primary Contact: ` (bold)
* **Secondary Contact** — prefixed `Secondary Contact: ` (bold) show `N/A` if empty or country code only
* **Top-right action icons:** Edit (blue `#5B8FF9`) and Delete (red `#FE7062`). Icons have `title` tooltips and are 40px circular touch targets.

All text uses clear spacing; truncated content should ellipsize to avoid overflow.

---

## Sample Data

* Include **16 sample employees** seeded into `localStorage['employees']` with fields: `id, fullName, employeeId, role, employeeType, company, primaryContact, secondaryContact` and other metadata as needed.

---

## Top Action Row & Search

* Fixed action row at top-right with three circular icon buttons (40px, white background, border `1px solid #D2D5DA`, subtle shadow):

  * **Filter** — opens Mobile Filter Dialog.
  * **Export** — shows tooltip "Export" (no export implementation required).
  * **Add** — navigates to `http://127.0.0.1:5500/operations/employee-management/add.html` and shows an alert; `title` tooltip "Add".
* Below the action row, a full-width **Search bar** (white background, border `1px solid #D2D5DA`, border-radius `8px`, padding `12px 16px`, height `48px`) with a magnifying glass icon at the start and placeholder **"Search employees..."**. Search filters name, ID, role, and contacts in real time with debounce.

---

## Mobile Filter Dialog

* Popover anchored to top-right, width `320px`, white background, `border-radius: 8px`, padding `16px`, `box-shadow: 0 4px 12px rgba(0,0,0,0.15)`, with backdrop `rgba(0,0,0,0.4)`.
* Header: **FILTERS** and blue **RESET** button; Close X button top-right.
* Filters in a two-column layout:

  * **Employee Type** (select)
  * **Roles** (select)
  * **Company** (select)
* Each control: label (`14px, font-weight 500`) and native select (`width: 240px; border: 1px solid #D2D5DA; border-radius: 4px; padding: 8px 12px`).
* RESET clears all filters and resets page to 1.
* Clicking backdrop closes dialog.

---

## Pagination (Fixed Bottom Bar)

* Fixed bottom bar with background `#F1F3F7`, padding `12px 16px`, `box-shadow: 0 -2px 8px rgba(0,0,0,0.1)`, `z-index: 100`.
* Shows **Page X of Y** text (12px gray) and centered pagination controls:

  * **Previous/Next** buttons (white when enabled, gray `#E0E0E0` disabled) bordered `1px solid #D2D5DA`.
  * Circular page buttons (32px): active `#2196f3` with white text, inactive transparent with border `1px solid #ddd`.
  * 10 cards per page; maximum 5 page buttons visible.

---

## Empty State

* If no employee records matched, show centered message:

  * Title: **No records found** (18px bold)
  * Subtitle: **Try adjusting your search or filter criteria** (14px gray)

---

## Actions & Behavior

* **Edit**: navigate to `http://127.0.0.1:5500/operations/employee-management/edit/{employeeId}.html`.
* **Delete**: show confirmation modal/dialog: **"Are you sure you want to delete {employeeName}?"** with Yes/No buttons. On Yes remove from `localStorage['employees']` and refresh list.
* **Export**: show an alert `Exporting employee data...` and `console.log` payload (no actual export required).
* **Add**: navigate to Add page and alert.
* **Filter**: opens dialog, filters combine with search.
* Search updates immediate with debounce (~250ms).
* Pagination recalculates based on filtered results.
* Only one dialog or modal open at a time; backdrop closes modal.

---

## Accessibility & UX

* Tooltips via `title` attributes.
* Large touch targets (40px) and keyboard-accessible controls.
* Smooth transitions (0.2–0.3s) for open/close animations and hover states.
* Use `aria-*` attributes where appropriate.

---

## Output

Produce a **single self-contained HTML file** that includes:

* Inline CSS and JS
* 16 sample employee records in `localStorage` for immediate testing
* All described UI, filters, pagination, search, and action behavior
## Mock Employee Card Data

Here is sample mock data for 16 employee cards:

```json
[
  {
    "id": "EMP001",
    "name": "John Abraham",
    "role": "Technician",
    "employeeType": "Full-Time",
    "company": "Prime Auto Garage",
    "primaryContact": "+971-9876543210",
    "secondaryContact": "",
    "designation": "Senior Technician"
  },
  {
    "id": "EMP002",
    "name": "Maria George",
    "role": "Supervisor",
    "employeeType": "Full-Time",
    "company": "Prime Auto Garage",
    "primaryContact": "+971-9234567810",
    "secondaryContact": "+971-9234567890",
    "designation": "Workshop Supervisor"
  },
  {
    "id": "EMP003",
    "name": "Liam Thomas",
    "role": "Manager",
    "employeeType": "Contract",
    "company": "Bright Motors LLC",
    "primaryContact": "+971-9988776655",
    "secondaryContact": "",
    "designation": "Service Manager"
  },
  {
    "id": "EMP004",
    "name": "Sophia Mathew",
    "role": "Advisor",
    "employeeType": "Full-Time",
    "company": "Prime Auto Garage",
    "primaryContact": "+971-9234876510",
    "secondaryContact": "",
    "designation": "Service Advisor"
  },
  {
    "id": "EMP005",
    "name": "Kevin Paul",
    "role": "Technician",
    "employeeType": "Part-Time",
    "company": "AutoXperts",
    "primaryContact": "+971-9345678123",
    "secondaryContact": "",
    "designation": "Technician"
  },
  {
    "id": "EMP006",
    "name": "Emily Rose",
    "role": "Supervisor",
    "employeeType": "Full-Time",
    "company": "AutoXperts",
    "primaryContact": "+971-9456123780",
    "secondaryContact": "+971-9456123700",
    "designation": "Shift Supervisor"
  },
  {
    "id": "EMP007",
    "name": "Noah Varghese",
    "role": "Technician",
    "employeeType": "Full-Time",
    "company": "Bright Motors LLC",
    "primaryContact": "+971-9944332211",
    "secondaryContact": "",
    "designation": "Auto Electrician"
  },
  {
    "id": "EMP008",
    "name": "Ava Johnson",
    "role": "Advisor",
    "employeeType": "Contract",
    "company": "Prime Auto Garage",
    "primaryContact": "+971-9556677880",
    "secondaryContact": "",
    "designation": "Customer Advisor"
  },
  {
    "id": "EMP009",
    "name": "Ethan Joseph",
    "role": "Technician",
    "employeeType": "Full-Time",
    "company": "SpeedyFix",
    "primaryContact": "+971-9123456781",
    "secondaryContact": "",
    "designation": "Mechanical Technician"
  },
  {
    "id": "EMP010",
    "name": "Isabella Grace",
    "role": "Manager",
    "employeeType": "Full-Time",
    "company": "SpeedyFix",
    "primaryContact": "+971-9234001987",
    "secondaryContact": "",
    "designation": "Operations Manager"
  },
  {
    "id": "EMP011",
    "name": "Daniel Mathews",
    "role": "Supervisor",
    "employeeType": "Contract",
    "company": "AutoCare Pro",
    "primaryContact": "+971-9988223344",
    "secondaryContact": "",
    "designation": "Floor Supervisor"
  },
  {
    "id": "EMP012",
    "name": "Olivia Thomas",
    "role": "Technician",
    "employeeType": "Full-Time",
    "company": "AutoCare Pro",
    "primaryContact": "+971-9099887766",
    "secondaryContact": "",
    "designation": "Dent & Paint Technician"
  },
  {
    "id": "EMP013",
    "name": "William Peter",
    "role": "Advisor",
    "employeeType": "Part-Time",
    "company": "Prime Auto Garage",
    "primaryContact": "+971-9554321009",
    "secondaryContact": "",
    "designation": "Maintenance Advisor"
  },
  {
    "id": "EMP014",
    "name": "Amelia Joy",
    "role": "Manager",
    "employeeType": "Full-Time",
    "company": "AutoXperts",
    "primaryContact": "+971-9332211008",
    "secondaryContact": "",
    "designation": "General Manager"
  },
  {
    "id": "EMP015",
    "name": "James Antony",
    "role": "Technician",
    "employeeType": "Contract",
    "company": "Bright Motors LLC",
    "primaryContact": "+971-9445566770",
    "secondaryContact": "",
    "designation": "AC Technician"
  },
  {
    "id": "EMP016",
    "name": "Charlotte Daniel",
    "role": "Supervisor",
    "employeeType": "Full-Time",
    "company": "SpeedyFix",
    "primaryContact": "+971-9776655443",
    "secondaryContact": "",
    "designation": "Lead Supervisor"
  }
]
```
---
## Image
<img src='./assets/Screenshot 2025-11-20 135953.png'>
<img src='./assets/Screenshot 2025-11-20 140055.png'>
<img src='./assets/Screenshot 2025-11-20 140119.png'>