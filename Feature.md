# Add Vehicle Form

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) that implements an **Add Vehicle Form**. The form must be responsive and saved at:

```
http://127.0.0.1:5500/app/management/vehicle/add.html
```

---

## Layout & Responsiveness

* **Desktop (≥1200px):** two-column grid.
* **Tablet (≤1200px):** container width 80% and single-column layout.
* **Mobile (≤728px):** single-column, full-width form groups.
* **Small devices (≤600px):** country-code dropdown stacks above phone input; buttons wrap under 500px and become full-width under 436px.
* Page background: `#F1F3F7`.
* Card background: `#E5E8FF`, shadow `0px 4px 4px rgba(0,0,0,0.25)`, border-radius `10px`.
* Inputs: white background, border `2px solid #D2D5DA`, font-family Helvetica, focus accent `#1c6ead`.

---

## Fields

**Required unless stated otherwise**

* **Plate No.** (text) — no spaces, max 30, unique across `localStorage.vehicleAccounts` (prevent duplicates).
* **VIN** (text) — max 30.
* **Vehicle Brand** (searchable dropdown) — 10+ hardcoded brands sorted alphabetically; creatable (modal). Selecting a brand populates the **Vehicle Model** dropdown.
* **Vehicle Model** (dropdown) — populated after brand selected; max 30; creatable only when brand chosen.
* **Owner First Name** (required)
* **Owner Last Name** (required)
* **Primary Contact** (country-code dropdown + number input) — required; country-code dropdown with flags for 10 countries (default `+971` UAE); number 9–15 digits; store as `+971-501234567`.
* **WhatsApp Contact** (country-code + number) — optional; if provided must be 9–15 digits.
* **Email** (required) — max 50, validate email format.
* **Company Fleet Name** (optional)

### Additional Fields (collapsed accordion)

* Model Year
* Engine Capacity
* Color
* Emirates
* Insurance
* Claim No
* LPO No

Accordion must expand/collapse with smooth animation.

---

## Buttons & Navigation

* Bounce back arrow top-left linking to:

```
http://127.0.0.1:5500/app/managementmanagement/vehicle/table.html
```

* Bottom centered buttons (three):

  * **Save** — validates required fields, prevents duplicate plates, saves new vehicle to `localStorage.vehicleAccounts` as an object with timestamps, shows success toast, then navigates to vehicle list.
  * **Job Card** — validates & saves (if validation passes) then navigates to job card page for the new vehicle: `http://127.0.0.1:5500/app/management/vehicle/jobcard/{vehicleId}.html` (simulate navigation/alert).
  * **Cancel** — returns to vehicle list without saving.

Buttons show spinner (100px rotating) during save operations.

---

## Create Brand/Model Modal

* Modal allows:

  * Adding a **new brand** with multiple models at once.
  * Adding **new models** to an existing brand.
* New entries saved in `localStorage.customBrands` and immediately merged with hardcoded brands, updating dropdowns and pre-selecting newly created values.
* Prevent duplicate brand/model entries (show inline error/toast).

---

## Data Storage & Format

* Vehicles saved under `localStorage.vehicleAccounts` as an array. Each saved object should include:

  * `id` (generated unique id)
  * `plateNo`
  * `vin`
  * `brand`
  * `model`
  * `ownerFirstName`
  * `ownerLastName`
  * `primaryContact` (stored `+code-number`)
  * `whatsappContact` (stored `+code-number` or `null`)
  * `email`
  * `companyFleet`
  * `additionalFields` (object with modelYear, engineCapacity, color, emirates, insurance, claimNo, lpoNo)
  * `createdAt` (ISO timestamp)
  * `updatedAt` (ISO timestamp)

* Custom brands stored as `localStorage.customBrands` as an object mapping brand → [models]. On load, merge with hardcoded brands.

---

## Validation Rules

* Required fields must be filled; show inline red error messages under invalid fields.
* Plate No: no spaces; max 30; must be unique.
* VIN: max 30.
* Brand required; Model required once brand selected.
* Primary Contact: 9–15 digits (number input); show error: "Please check your primary mobile number and try again." if invalid.
* WhatsApp: if provided, 9–15 digits.
* Email: valid format, max 50.
* Prevent creating duplicate brands/models.

All validation runs on Save/Job Card click (not live), and errors show toast and inline messages.

---

## UX Details

* Show toasts for errors and success (top-right, auto-dismiss 3s).
* During save/show spinner, disable inputs.
* On successful save, navigate to vehicle list and log the saved object to console.
* The Job Card button after saving should navigate to the job card creation page for that vehicle.

---

## Brands & Models

* Include 10+ hardcoded brands (sorted alphabetically) with sample models. Merge these with any `localStorage.customBrands` at runtime.

---

## Accessibility & Keyboard

* Modal and accordion accessible via keyboard.
* Country code dropdown accessible and labeled.

---

## Output

Produce a single file `add.html` containing all HTML, CSS, and JavaScript inline, implementing the features above.

Would you like me to generate the full single-file implementation now?

---

## Image
<img src='./assets/Screenshot 2025-11-19 145008.png'>
<img src='./assets/Screenshot 2025-11-19 145024.png'>