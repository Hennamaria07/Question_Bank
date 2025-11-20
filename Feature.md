# Add Suppliers 

## Overview

Create a **single-page Add Suppliers** interface for the fleet management app at the route:

```
/app/settings/suppliers/:userId/add
```

Replace `:userId` with the current logged-in user's id. The page stores temporary suppliers in `localStorage` under `tempSuppliers` and final suppliers under `suppliers`.

Reference image (optional):

```
/mnt/data/1553f955-955f-4642-91f4-74dc45e7f61e.png
```

---

## Layout

* **Header**: back-arrow (←) at top-left that navigates to `/app/settings/suppliers/:userId` and the page title **Add Suppliers**.
* **Main content**: two responsive sections inside a centered card with padding, rounded corners, and shadow:

  * **Left (form)** — `flex: 3` — Add Supplier form.
  * **Right (preview list)** — `flex: 2` — Temporarily added suppliers displayed as cards. This section is only visible when there is at least one supplier in `tempSuppliers`.

### Responsive behavior

* **Desktop / wide**: two-column layout — form left, preview right.
* **Mobile (<768px)**: stacked vertically **with the suppliers list appearing above the form**.

---

## Form Fields (all required)

* Supplier Name — text input
* Supplier ID — **exactly 8 characters** (text input)
* Address Line 1 — text input
* Address Line 2 — text input
* Contact Number — composed of:

  * Country code dropdown (default `+971` UAE; other options: `+1` USA, `+44` UK, `+91` India)
  * Phone number input (digits only, 9–15 digits)

> Every field must show a red asterisk (*) as required. Input validation messages appear below fields in red (#DC2626).

---

## Buttons & Actions

* **Add** (in the form): when clicked, validate all fields; if valid, append the supplier object to `tempSuppliers` in `localStorage` and render a supplier card on the right. Do **not** persist to `suppliers` yet.
* **Each supplier card** has a close (×) icon at the top-right — clicking removes that supplier from `tempSuppliers` and updates localStorage and UI.
* **Save All** (appears at the bottom of the right preview section when one or more temp suppliers exist): validates that at least one supplier exists, merges `tempSuppliers` into existing `suppliers` array in localStorage (deduplicating if desired), clears `tempSuppliers`, shows success alert, and navigates back to `/app/settings/suppliers/:userId`.
* **Back arrow**: when clicked, if `tempSuppliers` is non-empty, prompt a confirmation dialog warning about losing unsaved changes; if user confirms, navigate back, otherwise stay on page.
* **Cancel** (optional) in the form resets the form fields.

---

##localStorage

* **tempSuppliers** (temporary array stored in localStorage):

```js
[
  {
    id: 'TS-1635500000', // local id (timestamp-based or UUID)
    name: 'Supplier A',
    supplierId: 'ABCD1234',
    address1: '123 Main St',
    address2: 'Unit 4',
    countryCode: '+971',
    phone: '501234567',
    fullContact: '+971-501234567'
  },
  ...
]
```

* **suppliers** (final persistent array): similar structure. `Save All` merges `tempSuppliers` into this key.

All localStorage reads/writes must use `JSON.parse()` / `JSON.stringify()` inside `try/catch` blocks and show toasts or alerts on failure.

---

## Validation Rules

* All fields are required.
* Supplier ID must be exactly **8 characters**; otherwise show inline error: **"Supplier ID must be 8 characters"**.
* Contact number (phone input) must be **9–15 digits**; show error: **"Please enter a valid phone number (9–15 digits)"**.
* Country code dropdown must have a value (default `+971`).
* On Add, if validation fails, focus the first invalid field and show appropriate inline error messages in red (#DC2626).

---

## UI & Styling

* Page background: `#F1F3F7`.
* Form and preview card background: `#E5E8FF`, rounded corners `10px`, box-shadow for depth.
* Inputs: white background `#FFFFFF`, border `2px solid #D2D5DA`, border-radius `6px`.
* Add button: background `#91B3FA` (light blue).
* Save All button: background `#2A00B2` (dark purple), white text.
* Cancel button: white background.
* Temporary supplier cards: background `#F2F2F2`, rounded corners, padding, show supplier details with name as heading.
* Error messages: color `#DC2626`.

---

## User Flow Example

1. User fills in form fields and clicks **Add**.
2. Form validates fields; if valid, the supplier object is appended to `tempSuppliers` and saved in localStorage.
3. The right-side preview appears (if it wasn't visible) showing cards for each temp supplier.
4. User may remove cards by clicking × — that updates `tempSuppliers` immediately.
5. When ready, the user clicks **Save All** which merges temp suppliers into `suppliers` and navigates back to the suppliers list.

---

## Edge Cases & Notes

* If `tempSuppliers` already exists on page load, pre-populate the preview list from localStorage so users don't lose progress on refresh.
* Consider de-duplicating supplier IDs on Save All (optional but recommended): if a supplier with the same `supplierId` exists in `suppliers`, either skip or update it — decide behavior and document it in UI (e.g., show a confirmation).
* Navigation must include the `:userId` path; ensure the back arrow constructs the URL correctly.

---

## Accessibility

* Provide `aria-label` on the back arrow and close icons.
* Ensure form labels are associated with inputs.
* Keyboard accessible controls for adding/removing cards and Save All.

---

## Output

Produce a single self-contained HTML file (inline CSS + JS) implementing the above behavior and persisting data to `localStorage` under the keys `tempSuppliers` and `suppliers`.

---
## Image
<img src='./assets/Screenshot 2025-11-20 124824.png'>
<img src='./assets/Screenshot 2025-11-20 125223.png'>