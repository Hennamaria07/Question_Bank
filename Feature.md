# Edit Supplier

Create a **single self-contained HTML file** (HTML + CSS + vanilla JavaScript) to **edit an existing supplier**. The page reads from `localStorage.suppliers` and **auto-populates the form with the selected supplier's data by default**, allowing users to update supplier details. The UI should be **responsive, clean, and purple-themed**.

---

## Navigation & Header

* Page URL: `/app/settings/suppliers/edit/:supplierId.html`  
  `:supplierId` is the ID of the supplier being edited.
* Header:
  * Back arrow (←) navigates to `/app/settings/suppliers/:userId.html`
    * Shows a **confirmation dialog** if there are unsaved changes
  * Page title: `"Edit Supplier"`

---

## Form Layout

* Single centered form:
  * Max width: 800px
  * Background: `#E5E8FF`
  * Responsive padding (reduced on screens <768px)
* Top dropdown selector:
  * Label: `"Select Supplier to Edit *"`
  * Populates from `localStorage.suppliers`
  * Option format: `"Supplier Name (SupplierID)"`
* If no suppliers exist:
  * Hide the form
  * Show centered gray message: `"No suppliers found. Please add suppliers first."`
* **Auto-population**:
  * On page load, the form should automatically fill all fields with the selected supplier’s existing data from localStorage:
    * Supplier Name
    * Supplier ID
    * Address Line 1
    * Address Line 2
    * Contact Number (split into country code and number)
    * Active status

---

## Form Fields

* Supplier Name (required)
* Supplier ID (required, exactly 8 characters)
* Address Line 1
* Address Line 2
* Contact Number:
  * Stored as `"countryCode-number"` in localStorage
  * Split into:
    * Country code dropdown: `+971 UAE`, `+1 USA`, `+44 UK`, `+91 India`
    * Number input field
* Active Status:
  * Custom toggle switch:
    * Width: 50px, Height: 24px
    * White circular slider moves left/right
    * Gray background (`#ccc`) when inactive
    * Green background (`#4CAF50`) when active
  * Label dynamically displays `"Active"` / `"Inactive"`

---

## Buttons

* **Update** (dark purple: `#2A00B2`)
* **Cancel** (white)
  * Navigates back to `/app/settings/suppliers/:userId.html`
  * Shows confirmation dialog if unsaved changes

---

## Validation Rules

* All required fields must be filled
* Supplier ID must be **exactly 8 characters**
* Contact number must be **9–15 digits**
* Error messages appear **below each field** in red (`#DC2626`)
* On successful validation:
  * Update supplier object in `localStorage.suppliers`
  * Include name, supplierId, address lines, contact, and active status
  * Show **success alert**: `"Supplier updated successfully!"`
  * Refresh dropdown options (keep current supplier selected)
  * Do not navigate away

---

## UI & Styling

* White input fields
* Borders: `#D2D5DA`
* Input height: 42px
* Proper spacing between fields
* Responsive for mobile:
  * Form and inputs adjust width and padding below 768px

---

## Mock Data Example

```js
if (!localStorage.suppliers) {
  localStorage.suppliers = JSON.stringify([
    {
      _id: "SUP001",
      name: "Alpha Traders",
      supplierId: "SUPP0001",
      contactNumber: "+971-501234567",
      addressLine1: "Business Bay, Dubai",
      addressLine2: "Office 101",
      active: true,
      userId: "user123"
    },
    {
      _id: "SUP002",
      name: "Beta Supplies",
      supplierId: "SUPP0002",
      contactNumber: "+971-502345678",
      addressLine1: "Deira, Dubai",
      addressLine2: "Warehouse 5",
      active: false,
      userId: "user123"
    }
  ]);
}
```

## Image
<img src='./assets/Screenshot 2025-11-20 114758.png'>