# Edit Vehicle Form — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) that implements an **Edit Vehicle Form**. The page must use the same layout, styles, and responsive behavior as the Add form and pre-populate fields from `localStorage`.

This page will live at a route like:

```
/app/management/vehicle/edit.html?vehicleId={vehicleId}
```


## Loading & Data Fetching

* On `DOMContentLoaded`, read the `vehicleId` from the URL (path or query parameter as appropriate).
* Show a centered rotating **loading spinner** (100px diameter border animation) while fetching data from `localStorage['vehicleAccounts']`.

  * Spinner styling: rotating border with colors `#5f8edb` and `#3B82F6`.
* If the `vehicleId` is not found, show an error toast: **"Vehicle not found"** and redirect to the vehicle list page.
* If found, pre-populate the form fields with the stored vehicle object and hide the spinner.

---

## Layout & Visuals

* Use the **same three-column layout** as the Add form (left/middle/right) and identical styling:

  * Card background `#E5E8FF`, inputs white `#FFFFFF` with border `2px solid #D2D5DA`.
  * Buttons, spacing, fonts and responsive breakpoints must match the Add form.
* Back arrow at top-left that navigates to:

```
/app/management/vehicle/table/{vehicleId}
```

---

## Form Fields (pre-populated)

All fields mirror the Add form but are pre-filled with saved values from the matched `vehicleAccounts` entry.

### Primary Fields

* **Plate No.** — pre-filled, editable. Validation: no spaces allowed, max 30 characters.
* **VIN** — pre-filled, editable, max 30 characters.
* **Vehicle Brand** — dropdown, pre-selected. Changing brand filters & resets the **Model** dropdown.
* **Vehicle Model** — dropdown populated based on the selected brand; pre-selected to stored model.
* **First Name** — pre-filled, max 30 characters.
* **Last Name** — pre-filled, max 30 characters.
* **Primary Contact Number** — stored as string like `+971-9876543210`; split on `-` to pre-select country code dropdown and fill the number input (validate 9–15 digits).
* **WhatsApp Contact Number** — same split behavior; if stored value contains only country code like `+971-` display empty number input.
* **Email** — pre-filled, max 50 chars, must be valid format.
* **Company Fleet Name** — pre-filled if exists.

### Additional Fields (Accordion)

Collapsed by default; expandable with smooth animation.

* **Model Year**
* **Engine Capacity**
* **Color**
* **Emirates**
* **Insurance**
* **Claim No**
* **LPO No**

All of the above pre-filled if existing in the stored object.

---

## Buttons & Actions

* **Update** (primary): replaces Save from Add form.

  * Background `#2A00B2`, white text, same dimensions and styling as Save.
  * On click: validate the form (rules below), then update the matching vehicle object in `localStorage['vehicleAccounts']` by `id`:

    * Preserve `createdAt`.
    * Add/update `updatedAt` with current datetime (ISO string).
    * Merge changes into existing object.
  * On successful update: show success toast **"Vehicle updated successfully"** and navigate to the vehicle list.
* **Job Card**: performs the same validation and update as Update, then navigates to the job card creation flow (same as Add behavior).
* **Cancel**: navigates back to the vehicle list without saving.

All navigations should use `window.location.href`.

---

## Brand & Model Dialogs

* Allow creating new brand/model pairs via a dialog identical to Add form's Brand/Model dialog.
* Newly created brand/model entries are saved to `localStorage['customBrands']` (or merge with existing store) and immediately refresh the brand and model dropdowns, selecting the newly created item.
* Prevent duplicate brand/model entries.

---

## Country Code Handling

* Country code dropdowns must contain ~50 country codes with flags and sorted names.
* When pre-populating contact fields, split stored strings by `-`:

  * Example: `+971-9876543210` → country code `+971` pre-selected, number `9876543210` populated.
  * If stored WhatsApp is `+971-` or `+971` (no number), show the dropdown pre-selected and an empty number input.

---

## Validation Rules

* **Plate No.**: required, no spaces, ≤ 30 characters.
* **VIN**: required, ≤ 30 characters.
* **First/Last Name**: required, ≤ 30 characters each.
* **Email**: optional? (match Add form behavior) — if provided, must be valid and ≤ 50 chars.
* **Primary Contact**: required, numeric, 9–15 digits (after splitting country code). Show specific inline error: **"Please check your primary mobile number and try again."**
* **WhatsApp**: optional; if provided, same validation as primary.
* **All fields must not exceed max lengths**; show inline red error messages under each invalid field.
* On submit, if any required validation fails, show an overall error toast describing the issue.

---

## Update Behavior & Edge Cases

* Preserve `id` and `createdAt` when saving; set or update `updatedAt`.
* If the user changes the brand, the model dropdown must reset (clear selection) and require a valid model selection before saving.
* If user creates a new brand/model during edit, update dropdowns immediately and select the new values.
* If the provided `vehicleId` is not found, show an error toast and redirect to the list page.

---

## UX & Accessibility

* Loading spinner centered and visible until DOM is populated.
* Smooth transitions (300ms) for dropdowns, accordion expand/collapse, dialog open/close.
* Country dropdowns should show flags and be keyboard accessible.
* Keyboard focus management: focus first input after load; trap focus within dialogs while open.

---

## Storage & API Surface

* `localStorage['vehicleAccounts']`: array of vehicle objects. Update by finding the object with `id === vehicleId` and replacing/merging.
* `localStorage['customBrands']`: array for user-added brands/models.
* Wrap all `localStorage` reads/writes in `try/catch` and show toasts on failure.

Example vehicle object shape:

```json
{
  "id": "VH-001",
  "plateNo": "KL-07-AB-1234",
  "vin": "1HGCM82633A004352",
  "brand": "Toyota",
  "model": "Camry",
  "firstName": "John",
  "lastName": "Doe",
  "primaryContact": "+971-9876543210",
  "whatsapp": "+971-9876543210",
  "email": "john.doe@example.com",
  "companyFleet": "ABC Motors",
  "additional": { "modelYear": "2019", "engineCapacity": "2.5L" },
  "createdAt": "2025-07-01T12:00:00.000Z"
}
```

---

## Feedback & Toasts

* Use top-center toast notifications for success (green) and errors (red), auto-dismiss after 3s.
* Provide inline field-level error messages in red for validation failures.

---

## Output

Produce a **single self-contained HTML file** (e.g., `edit.html`) with inline CSS and JavaScript that implements the Edit Vehicle.

---
## Image
<img src='./assets/Screenshot 2025-11-20 132750.png'>
<img src='./assets/Screenshot 2025-11-20 132814.png'>
