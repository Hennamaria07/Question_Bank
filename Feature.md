# Add Employee Profile

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) for an **Add Employee Profile** page designed primarily for desktop (1024px and above). The page must be responsive and include a navigation link back to the Employee Management list.

Target URL for the page:

```
http://127.0.0.1:5500/operations/employee-management/add.html
```

Reference image (uploaded):

```
/mnt/data/1553f955-955f-4642-91f4-74dc45e7f61e.png
```

---

## Layout

A **three-column** layout on desktop (≥1024px): left, middle, right.

### Left section (flex: 2)

* White background, padding `20px`, `min-width: 20rem`.
* Top-left: a bouncing back-arrow icon linking to the Employee Management list:

  * `http://127.0.0.1:5500/operations/employee-management.html`
* Circular profile image placeholder (60% width of the left column).
* Text: **"New Employee"** and **"Not Assigned"** as the employee ID.

### Middle section (flex: 3)

* `min-width: 50rem`, left border `1px solid #ddd`.
* Header: **"Profile View"**.
* Form fields:

  * **Full Name** — required (red asterisk).
  * **Employee ID** — required, **no spaces allowed**.
  * **Password** — auto-generated as `randomNumber_employeeId`, **read-only**, click-to-copy feature; clicking copy icon turns icon green for 5 seconds.
  * **Primary Contact Number** — required; country code dropdown with flags for ~50 countries (default `+971` UAE); input restricted to **9–15 digits**.
  * **Secondary Contact Number** — optional, same format if entered.

### Right section (flex: 1)

* Left border `1px solid #ddd`.
* Header: **"Profile Settings & Privileges"**.
* Form controls:

  * **Role** dropdown — required: Technician, Supervisor, Manager, Advisor.
  * **Authorization** checkboxes arranged in a 4-column grid:

    * Dashboard, Services, Services Overview, Approvals (these four must be auto-checked and disabled for Manager and Advisor roles).
    * Manual Time Entry, Employee Management, Vehicle Management, Settings.
    * *Conditional:* exclude Vehicle Management if a `vehicleMgmt` config flag is `false`.
    * *Conditional:* exclude Services and Manual Time Entry if a `timeMgmt` config flag is `false`.
  * **Reports** checkboxes: Vehicle Report, Employee Report.
  * **Select Entry Page** dropdown — required; populated dynamically from checked authorizations (exclude Approvals from options).
  * **Designation** dropdown: Technician, Supervisor, Manager, Foreman, Other — if Other selected, show an **Add Designation** text input (required).
  * **Employee Type** dropdown: Permanent, Contract, Temporary — if **Contract** is selected, show **Company** dropdown (required) with options: ABC Motors, XYZ Auto, Premium Cars, Elite Service, Other — if Other selected, show **Add Company** text input (required).

---

## Buttons

* Bottom center: **Save** and **Cancel** buttons.
* **Save**: `background: #2A00B2`, white text, `width: 127px`, `height: 48px`, `border-radius: 10px`, shadow `0px 4px 4px rgba(0,0,0,0.25)`.
* **Cancel**: white background, border, same dimensions.
* Cancel navigates to the Employee Management list without saving.

---

## Validation Rules

* All required fields must be filled; invalid fields should display inline errors.
* **Employee ID**: must not contain spaces — otherwise show an inline error.
* **Primary Contact**: must be **9–15 digits**; otherwise show inline error: **"Please check your primary mobile number and try again."**
* **Secondary Contact**: if entered, must follow same validation as primary.
* If **Employee Type** = Contract and Company not selected (or Other but no value entered), show **"Company is required for Contractors"** or **"Additional Company/Designation information is required"** accordingly.
* Prevent duplicate entries in dropdowns when dynamically adding (e.g., Add Company or Add Designation).

---

## UX Details

* **Password generation**: create a `randomNumber_employeeId` value when Employee ID is provided (or on page load with a placeholder Employee ID). Show as read-only with a copy button.
* **Click-to-copy**: copy password to clipboard and flash the copy icon green for 5s.
* **Country code dropdown**: include flags and country names; default to `+971` (UAE). Input stores numbers as `+<code>-<number>` in saved data.
* **Authorization logic**: for Manager and Advisor roles, auto-check and disable Dashboard, Services, Services Overview, Approvals.
* **Select Entry Page**: dynamically list checked authorizations (exclude Approvals). This dropdown is required.

---

## Storage & Submission

* On successful validation, collect all form values into an object and append it into a JSON array stored in `localStorage` under key `employees`.
* Saved phone numbers must include country code, e.g., `+971-9876543210`.
* After saving, show success toast: **"Employee added successfully"**, then navigate to:

  * `http://127.0.0.1:5500/operations/employee-management.html`

---

## Styling & Theme

* Page background: `#F1F3F7`.
* Card background color: `#E5E8FF` with `box-shadow: 0px 4px 4px rgba(0,0,0,0.25)` and `border-radius: 10px`.
* Inputs: white background, border `2px solid #D2D5DA`, font-size `16px`.
* Labels color: `#6D7280`.
* Checkboxes: border `1px solid #ccc`, background `#f9f9f9`, hover `#e0e0e0`, checked accent `#2A00B2`.

---

## Responsiveness

* **≥1024px**: three-column layout as described. Profile image 60% width.
* **≤1020px**: sections stack vertically; profile image reduces to `100px` wide.
* **≤768px**: sections become full width with compact spacing.
* **≤600px**: checkboxes and country code dropdowns switch to single-column layout with the dropdown above phone input.

---

## Accessibility

* All form controls must have labels and appropriate `aria-` attributes.
* Keyboard accessible copy button, dropdowns, and checkboxes.

---

## Output

Produce a single file named `add.html` and place it at:

```
/operations/employee-management/add.html
```

All HTML, CSS, and JavaScript must be inline in this file.

---

## Image
<img src='./assets/Screenshot 2025-11-19 141911.png'>
<img src='./assets/Screenshot 2025-11-19 141935.png'>