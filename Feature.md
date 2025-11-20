# View Employee Profile — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) that implements a **View Employee Profile** page in read-only mode. The page must load an employee by `userId` from the URL (`/app/management/employees/view/:userId`) and display all profile details in a clean two-column layout on desktop and responsive stacks on smaller screens.

---

## Layout Overview

* **Two-column layout** for screens ≥ 1024px.

  * **Left section** (flex: 2, min-width: 20rem): white card with padding `20px`.
  * **Right section** (flex: 3, min-width: 50rem): main profile view card with header and read-only fields.
* No border-left between columns.
* Page background `#F1F3F7`; card background `#E5E8FF` with `box-shadow: 0px 4px 4px rgba(0,0,0,0.25)` and `border-radius: 10px`.

---

## Left Section (Profile Summary)

* White card area containing:

  * Circular profile image placeholder (60% width of the left card):

    * Desktop: `200px` diameter
    * Tablet: `150px`
    * Mobile: `100px`
  * **Update Authentication Image** button:

    * Background `#2A00B2`, white text.
    * On click: alert **"Face recognition update feature - Coming soon!"**.
  * Employee full name prominently in bold.
  * Employee ID displayed below name.
  * **QR code** section showing employee ID as plain text (no generation required).

---

## Right Section (Profile View — Read-only)

* Header: **Profile View** (prominent)
* Display employee fields as **disabled/read-only inputs** with the following styles:

  * Disabled input background: `#f9f9f9`
  * Border: `2px solid #D2D5DA`
  * Height: `42px`, padding `0 12px`, font-size `16px`
  * Label: font-size `16px`, font-weight `500`, color `#6D7280`

### Fields to display

* Full Name (disabled input)
* Employee ID (disabled input)
* Primary Contact Number (disabled) — display as `+<code> <flag> - <number>` if possible (e.g. `+971 🇦🇪 - 9876543210`)
* Secondary Contact Number (disabled) — show only if exists, otherwise show `Not specified`
* Selected Reports (display comma-separated text) — show only if employee has Reports role; otherwise `Not specified`
* Default Entry Page (disabled input showing menu name, not ID)
* Designation (disabled input)
* Employee Type (disabled input)
* Company (disabled input, only visible if Employee Type is `Contract`)

All inputs must be non-editable and visually indicate disabled state.

---

## Data Loading & Lookup

* On page mount (`DOMContentLoaded`):

  1. Read `userId` from the URL path or query parameter.
  2. Load `localStorage['employees']` (or `localStorage['employeesData']`) and find the employee object with `id === userId`.
  3. If not found: show error toast **"Employee not found"** and stop (optionally navigate away).
  4. If found: populate UI with employee data.

* For fields stored as IDs (roles, designation, employeeType, company, entryPage, authorizations):

  * Load reference collections from localStorage (e.g., `roles`, `designations`, `employeeTypes`, `companies`, `menuItems`).
  * Match the stored IDs and display the human-readable `name` values. If lookup not found, display `Not specified`.

* For phone numbers stored as strings like `+971-9876543210`:

  * Split on `-` delimiter, find the country code in `countries` reference (localStorage or embedded list) to show flag emoji or short name.
  * Display as `+971 🇦🇪 - 9876543210`.
  * If number part missing, show `Not specified`.

---

## Interaction & Behavior

* **Update Authentication Image** button: only interactive control — on click show alert **"Face recognition update feature - Coming soon!"**.
* No Save/Cancel or other edit controls on this page.
* Show a centered **loading spinner** while fetching and preparing data. The spinner should be visible until data is rendered.
* If fields are empty, display `Not specified` placeholder text.

---

## Styling & Responsiveness

* Desktop (≥1024px): two-column layout described above.
* ≤1020px: profile sidebar arranges horizontally with a `100px` image; sections stack vertically beneath header.
* ≤768px: sections become full width stacked vertically with compact spacing.
* ≤600px: profile sidebar stacks vertically with `150px` image and larger touch targets.
* Use smooth transitions (`transition: all 0.3s ease`) for layout changes.

---

## Accessibility

* Inputs have `aria-readonly` or `disabled` attributes.
* Provide `alt` text for profile image.
* Button has `aria-label`.
* Ensure color contrast for readability.

---

## Error Handling & Toasts

* Implement `createToast(message, type)` for top-center notifications. Use green background for success and red for errors.
* Wrap `localStorage` reads in `try/catch` and show an error toast if data cannot be parsed.

---

## Example Employee Object Shape

```json
{
  "id": "U1001",
  "fullName": "Anees K",
  "employeeId": "EMP010",
  "primaryContact": "+971-9876543210",
  "secondaryContact": "+971-9876500010",
  "roles": ["role_reports"],
  "authorizations": ["Dashboard","Services"],
  "entryPage": "Employee Management",
  "designation": "Technician",
  "employeeType": "Permanent",
  "company": "ABC Motors"
}
```

---

## Output

Produce a single self-contained HTML file with inline CSS and JavaScript implementing the above **View Employee Profile** read-only page. Use the uploaded reference image at:

---

## Image
<img src='./assets/Screenshot 2025-10-21 162724.png'>