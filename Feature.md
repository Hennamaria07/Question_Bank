# Service Add Form

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) that implements a responsive **Service Add Form** and will live at:

```
http://127.0.0.1:5500/dashboard/services/add.html
```

Design should use a purple theme, clean layout, and be responsive across desktop, tablet, and mobile breakpoints.

---

## Form Fields

### Read-only (pre-filled)

* **Plate No** (e.g. `KL-07-AB-1234`) — read-only
* **Brand** (e.g. `Toyota`) — read-only
* **Job Card ID** (e.g. `JC-2024-001`) — read-only
* **Advisor Name** (e.g. `John Smith`) — read-only


---

## Validation & Flow

1. On **Submit**, validate all required fields.

   * If any required field is empty or invalid, show inline error (red border + message) for each invalid field. Do not open modal.
2. If validation passes, open a centered **modal dialog** (Break Time Confirmation) with the following:

   * Title (centered): **"Did you work during break time?"** (font-size: 18px)
   * Bold subtitle (centered): **"Worked Time during Breaks"** (font-size: 16px)
   * Two inputs: **Hours** (number, >= 0) and **Minutes** (number, 0–59). Only numeric input allowed.
   * Two centered buttons at the bottom: **Yes** (saveButton) and **No** (cancelButton) with minimum width `100px`, `10px` gap.
3. If the user clicks **No** in the modal: close modal and navigate to `http://127.0.0.1:5500/dashboard/services.html` (without saving).
4. If the user clicks **Yes**:

   * Validate at least one of Hours or Minutes > 0. If both are zero or empty, show `alert("Please enter valid worked hours or minutes.")` and keep modal open.
   * If valid, save all form data + breakHours + breakMinutes + timestamp (ISO string) into `localStorage` under key `services` as an array (append new entry). Example object:

```json
{
  "plateNo": "ABC123",
  "brand": "Toyota",
  "jobCardId": "JC001",
  "advisorName": "John Doe",
  "supervisor": "supervisor1",
  "task": "oilChange",
  "description": "Routine maintenance",
  "breakHours": 1,
  "breakMinutes": 30,
  "timestamp": "2025-10-16T13:45:00.000Z"
}
```

5. After saving, reset the form and modal inputs (hours/minutes → 0) and navigate automatically to:

```
http://127.0.0.1:5500/dashboard/services.html
```

---

## UI / Styling Requirements

* **Required field error style**: `border: 2px solid red;` and error text `font-size: 12px; color: red;` under the field.
* **General layout**

  * Font family: `Helvetica, "Helvetica Neue", Arial, sans-serif`.
  * Clean spacing and readable typography.
* **Desktop (min-width: 1200px)**

  * Container width: `50%`, centered with `margin: 130px auto`.
  * Use a **two-column grid** layout for form fields.
  * Padding: `20px`.
  * Labels: `font-size: 16px`.
  * Inputs: `font-size: 14px`.
  * Title (`h1`): `font-size: 24px`.
* **Tablet (max-width: 1200px)**

  * Single-column layout, width `90%`, `margin: 30px auto`.
* **Mobile (max-width: 728px)**

  * Single-column, full-width inputs.
* **Small Mobile (max-width: 600px)**

  * Modal stacks vertically, smaller font sizes (labels `14px`), centered inputs with `10%` side margin.
* **Modal styling**

  * Fixed centered: `top: 50%`, `left: 50%`, `transform: translate(-50%, -50%)`.
  * Background: white (or `var(--card-background-color)`).
  * Shadow: use `var(--card-shadow)`.
  * Border-radius: `10px`.
  * Padding: `20px`.

---

## Accessibility & Behavior

* Numeric-only inputs must prevent non-numeric keypresses except Backspace, Delete, Arrow keys, and Tab.
* Ensure keyboard accessibility for the modal (focus on first input, ESC to close optional).
* Use semantic HTML for labels and inputs.

---

## Output

Save the file as `add.html` and place it at:

```
/dashboard/services/add.html
```

All HTML, CSS, and JavaScript must be inline in the single file.

---

## Image

<img src='./assets/Screenshot 2025-11-19 135354.png'>
<img src='./assets/Screenshot 2025-11-19 135246.png'>


