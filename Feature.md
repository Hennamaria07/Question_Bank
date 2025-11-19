# Add Job Order — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) that implements an **Add Job Order** page. The page should be responsive and follow the visual style described below (purple-accent, clean layout). The file should use `dayjs` (included inline or via CDN) for date/time formatting and validation.

---

## Location & Mode

* The page is for **Add** mode and the URL path will include `/add`.
* On successful save, navigate back to:

```
http://127.0.0.1:5500/operations/vehicle-management.html
```

---

## Visual Layout

* Title at top-left: **Job Order** (font-size: 24px; font-weight: 600; color: #232323; margin-bottom: 25px).
* Card container styling:

  * `margin: 0 50px; padding: 20px; background: #E5E8FF; border-radius: 8px; box-shadow: 0px 4px 4px rgba(0,0,0,0.25)`.
* Inputs: white background `#FFFFFF`, border `2px solid #D2D5DA`, border-radius consistent, readable font sizes.

### Responsive breakpoints

* Desktop: margin `0 50px`, padding `20px`.
* Tablets (770–1104px): margin `0 30px`, padding `15px`.
* Mobile (<768px): single-column layout, margin `0 10px`, padding `10px`.
* Very small (<480px): reduced font sizes for compactness.

---

## Read-only Vehicle & Customer Info (top section)

Display these read-only fields populated from localStorage or URL param (vehicleId):

* Plate No.
* Vehicle — brand + model (with a car icon)
* Customer Name
* Email
* Primary Contact
* WhatsApp — **hidden** when empty or only contains country code

---

## Job Card Inputs

### Job Card

* Read-only initially showing: **"Will be generated on save"**.
* On save generate `jobCardId` with format:

  * `JC-NBW-{DDMMYYYY}-{5-digit-sequence}`
  * Sequence is the next number from the latest stored sequence in localStorage (maintain a counter, e.g., `jobCardSeq_{DDMMYYYY}` or global `jobCardSeq`), zero-padded to 5 digits.

### Arrival Date (required)

* Date picker using `dayjs` format `DD-MM-YYYY`.
* Default to today's date (set via JS on load).
* Style: `2px solid #D2D5DA`, border-radius `4px`, height `40px`.
* Enforce min/max rules via JS as required.

### Estimated Delivery Date (required)

* Dayjs-based date picker with `DD-MM-YYYY` formatting.

### Estimated Delivery Time (required)

* Time picker with `HH:MM AM/PM` format (use a simple select or custom time input).

### Mileage (required)

* Numeric input.
* On input: strip commas and Arabic numerals (convert Arabic-Indic digits to Western digits), prevent mouse wheel changes.
* Validate with regex `/^\d*\.?\d{0,2}$/` (up to two decimals).
* On blur: format with comma separators using `Intl.NumberFormat`.

### Advisor (required)

* Dropdown populated from localStorage `usersData` filtered where `role === 'Advisor'`.

### Status (dropdown)

* Options: Draft, Job Card Created, In-progress, On Hold, Ready for Delivery, Completed, Cancelled.
* When status is changed to **On Hold** or **Cancelled**, show a conditional **Reason** text input — required for those statuses.

### Comments

* Full-width textarea for optional comments.

---

## Date/Time Handling

* Use `dayjs` for formatting and parsing dates/times.
* Display and parse `DD-MM-YYYY` for dates and `hh:mm A` for times.

---

## Validation & UX Details

* Show inline validation messages and toasts for summary errors.
* Disable mouse wheel on numeric fields to prevent accidental changes.
* Ensure WhatsApp field hides if value is empty or only a country code.
* Provide accessible form labels and `aria-*` attributes.

---

## Toast Notifications

* Appear top-center.
* Auto-dismiss after 3s.
* Use different styles for success (green) and error (red) with clear messages.

---

## Error Handling

* Wrap localStorage interactions in `try/catch` blocks.
* Show appropriate error toasts with actionable messages (e.g., "Failed to save job order — please try again").

---

## Sample localStorage Keys & Data Shape

* `usersData` — array of user objects (used to populate Advisor dropdown):

```js
[ { id: 'U1', name: 'Anees', role: 'Advisor' }, ... ]
```

* `jobOrderData_{vehicleId}` — array of saved job orders for a vehicle. Example object:

```js
{
  jobCardId: 'JC-NBW-05112025-00001',
  vehicleId: 'VH1001',
  plateNo: 'KL-07-AB-1234',
  advisor: 'Anees',
  arrivalDate: '05-11-2025',
  estDeliveryDate: '07-11-2025',
  estDeliveryTime: '10:30 AM',
  mileage: '12,345.00',
  status: 'Draft',
  comments: '',
  createdAt: '2025-11-05T08:00:00.000Z',
  jobCardLive: true
}
```

* `jobCardSeq` or `jobCardSeq_{DDMMYYYY}` — sequence counters for jobCardId generation.

---

## Accessibility

* Use semantic HTML elements and labels.
* Ensure focus order, keyboard navigation, and `aria` attributes for dynamic elements and toasts.

---

## Image
<img src='./assets/Screenshot 2025-11-19 150651.png'>
<img src='./assets/Screenshot 2025-11-19 150703.png'>