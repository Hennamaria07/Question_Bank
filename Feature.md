# Edit Employee Profile — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) for an **Edit Employee Profile** page that uses the same three-column responsive layout as the Add page. The page is designed primarily for desktop screens (≥1024px) but must be fully responsive and match the Add page’s visual style.

Target URL where this page will live:

```
/app/management/employees/edit/currentUserId.html
```

---

## Layout (three columns on desktop)

### Left column (flex: 2, min-width: 20rem)

* White card-style area with padding `20px`.

* Top-left: a bouncing back-arrow link that navigates to:

  ```
  /app/management/employees/currentUserId.html
  ```

* Circular profile image placeholder (60% width of left column).

* Display the employee's **Full Name** and **Employee ID** loaded from `localStorage` using the `userId` query parameter.

### Middle column (flex: 3, min-width: 50rem)

* Header: **"Profile View"**.
* Editable form fields (pre-filled from localStorage):

  * **Full Name** — editable, required.
  * **Employee ID** — **disabled/read-only** with gray background.
  * **Reset Password** checkbox — when checked, reveal a generated `randomNumber_employeeId` password field (read-only) with a copy icon that turns green for 5s when clicked. When unchecked, hide the new password field and keep the existing password unchanged.
  * **Primary Contact Number** — split the stored phone string (e.g., `+971-9876543210`) by `-` into a country code select and a number input (9–15 digits). Primary is required.
  * **Secondary Contact Number** — same behavior but optional; must handle the case where stored value may be only a country code or missing.

### Right column (flex: 1)

* Header: **"Profile Settings & Privileges"**.
* Controls pre-filled from saved employee data:

  * **Role** dropdown (required): Technician, Supervisor, Manager, Advisor.
  * **Authorization** checkboxes arranged in a 4-column grid:

    * Dashboard, Services, Services Overview, Approvals (these four are auto-checked and disabled for Manager and Advisor roles).
    * Manual Time Entry, Employee Management, Vehicle Management, Settings.
    * Conditional exclusions:

      * Exclude **Vehicle Management** if `vehicleMgmt` config flag is `false`.
      * Exclude **Services** and **Manual Time Entry** if `timeMgmt` config flag is `false`.
  * **Reports** checkboxes: Vehicle Report, Employee Report.
  * **Select Entry Page** dropdown — populated dynamically from checked authorizations except **Approvals**; required.
  * **Designation** dropdown; options include Technician, Supervisor, Manager, Foreman, Other — if **Other** is selected, show an **Add Designation** text input (pre-filled if employee previously had a custom designation).
  * **Employee Type** dropdown: Permanent, Contract, Temporary — if **Contract** is selected, show a **Company** dropdown (required) with options: ABC Motors, XYZ Auto, Premium Cars, Elite Service, Other — if **Other** is selected, show an **Add Company** text input (pre-filled if present).

---

## Data Loading & Initial UX

* On page load, show a centered **animated spinner** (loading state) while fetching the employee object from `localStorage`. Use the `userId` query parameter to locate the employee in an array stored under a key such as `employees`.

* If the employee is **not found**, show an error toast: **"Employee not found"** and navigate back to:

  ```
  /app/management/employees/currentUserId.html
  ```

* If found, pre-populate all form fields and UI state from the saved object and remove the loading spinner.

---

## Validation (same rules as Add page)

* On Save, validate the following client-side (and show toasts/errors):

  * Required fields must be filled; otherwise show toast: **"Please fill in all the required fields"**.
  * **Primary/Secondary phone** numbers must be 9–15 digits; when invalid show specific messages (e.g., **"Please check your primary mobile number and try again."**).
  * If **Employee Type** is **Contract**, the Company field must be selected (or additional company input provided); otherwise show **"Company is required for Contractors"**.
  * If **Designation** or **Company** is **Other** and the additional input is empty, show **"Additional Company/Designation information is required"**.
  * Prevent adding duplicate entries when adding a new Company or Designation (show an error like **"Company already exists"**).

---

## Password Reset Behavior

* If **Reset Password** is checked, generate a new password `randomNumber_employeeId`. Save the new password only if the user confirms Save.
* The password field is read-only and copyable. Clicking the copy icon copies the value to clipboard and turns the icon green for 5 seconds.

---

## Save Flow & Edge Cases

* On **Save**:

  1. Validate fields as described above.
  2. If the user is editing **their own profile** and is changing critical access (role or authorizations), show a confirmation prompt describing the change; only proceed if the user confirms.
  3. Update the employee object in the `employees` array in `localStorage`. Include the new password only if Reset Password was checked.
  4. Show success toast: **"Employee updated successfully"**.
  5. After a short delay, navigate to:

     ```
     /app/management/employees/currentUserId.html
     ```

* Handle secondary contact cases gracefully (e.g., if stored as only a country code, populate the select and leave number blank).

---

## Accessibility & UX

* Use labels, `aria-` attributes, and proper focus management (focus first field after load).
* Keyboard accessible copy and modal/confirm dialogs.

---

## Styling & Responsiveness

* Maintain the same styling rules as the Add page:

  * Card background: `#E5E8FF`, shadow `0px 4px 4px rgba(0,0,0,0.25)`, border-radius `10px`.
  * Inputs: white background, border `2px solid #D2D5DA`.
  * Labels color: `#6D7280`.

* Responsiveness:

  * **≥1024px**: three-column layout with 60% profile image in left column.
  * **≤1020px**: stack sections vertically; profile image reduces to `100px`.
  * **≤768px**: sections become full-width with compact spacing.
  * **≤600px**: checkboxes and country-code selects stack single-column and the country dropdown appears above the phone input.

---

## LocalStorage Key & Example Structure

* Employees are stored as an array under `localStorage['employees']`.
* Example employee object structure:

```json
{
  "id": "EMP010",
  "fullName": "Jaya M",
  "employeeId": "EMP010",
  "password": "12345_EMP010",
  "primaryContact": "+971-9876543210",
  "secondaryContact": "+91-9876500010",
  "role": "Technician",
  "authorizations": ["Dashboard","Services","Employee Management"],
  "reports": ["Vehicle Report"],
  "entryPage": "Employee Management",
  "designation": "Technician",
  "employeeType": "Permanent",
  "company": "ABC Motors"
}
```

---

## Output

* Produce a single self-contained HTML file (e.g., `edit.html`) containing all HTML, CSS, and JavaScript inline.
* The page must retrieve and update data in `localStorage` and handle navigation as described.

---

## Image
<img src='./assets/Screenshot 2025-11-19 143101.png'>
<img src='./assets/Screenshot 2025-11-19 142935.png'>
