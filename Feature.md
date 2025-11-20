# Suppliers Management

Create a **single self-contained HTML file** (HTML + CSS + vanilla JavaScript) for **managing suppliers**. The page stores and displays supplier records in `localStorage` and is designed to be **easy to use, responsive, and visually appealing**.

---

## Container & Layout

* Card-like container:
  * Padding: 16px
  * Background: `#F1F3F7`
  * Rounded corners and soft shadow
* Table layout:
  * Responsive
  * Pale header: `#D0D4F2`
  * Uppercase bold headings
  * Rounded first/last header corners
  * Alternating row colors: odd → `#F7F6FE`, even → `#FFFFFF`
  * Columns:
    * Supplier Name
    * Supplier Id
    * Address Line 1
    * Address Line 2
    * Contact Number
    * Status (Active/Inactive badge)
    * Actions (Edit button)
* On smaller screens:
  * Certain columns hide to keep layout readable
  * Table becomes horizontally scrollable if necessary

---

## Toolbar & Actions

* Top-right toolbar:
  * **Add button** navigates to `/app/settings/suppliers/add/{userId}.html`  
    (userId is derived from URL)
* Each row:
  * **Edit button** navigates to `/app/settings/suppliers/edit/{supplierId}.html`
  * Tooltips on action buttons
* Status badges:
  * `"Active"` → green badge
  * `"Inactive"` → red badge

---

## Features

### Data Handling

* On load:
  * Ensure `localStorage.suppliers` exists (array of objects):
    ```js
    {
      _id,
      name,
      supplierId,
      contactNumber,
      addressLine1,
      addressLine2,
      active, // true/false
      userId
    }
    ```
  * Load:
    * **Paginated slice** for table display
    * **Full list** for populating filter dropdowns

* All localStorage operations use:
  * `JSON.parse` / `JSON.stringify`
  * `try/catch` with graceful fallbacks

---

### Searching & Filtering

* **Live search**:
  * Filters rows by `name`, `supplierId`, `addressLine1`, `addressLine2`, or `contactNumber`
  * Resets page to 1 on change
* **Column filters**:
  * Supplier Name
  * Supplier Id
  * Dropdowns populated from full suppliers list
  * Reset button clears filters

---

### Pagination

* Simulated on client side
* Controls:
  * Rows per page: 10, 20, 30, 40
  * Previous / Next buttons
  * Page indicator: current page / total pages
  * Total count: “Showing X–Y of Z entries”
* Pagination updates dynamically with search/filters

---

### UI & Accessibility

* Loading spinner while fetching data
* Friendly message when no results: `"No records found / Try adjusting your search or filter criteria"`
* Hover and focus transitions on buttons
* Consistent padding and font sizes
* Responsive design for phones and tablets
* Visual cues:
  * Green badge for Active
  * Red badge for Inactive

---

## Example Mock Data

```js
// Initialize localStorage.suppliers if missing
if (!localStorage.suppliers) {
  localStorage.suppliers = JSON.stringify([
    {
      _id: "1",
      name: "Alpha Traders",
      supplierId: "SUP001",
      contactNumber: "+971501234567",
      addressLine1: "Business Bay, Dubai",
      addressLine2: "Office 101",
      active: true,
      userId: "user123"
    },
    {
      _id: "2",
      name: "Beta Supplies",
      supplierId: "SUP002",
      contactNumber: "+971502345678",
      addressLine1: "Deira, Dubai",
      addressLine2: "Warehouse 5",
      active: false,
      userId: "user123"
    },
    {
      _id: "3",
      name: "Gamma Corp",
      supplierId: "SUP003",
      contactNumber: "+971503456789",
      addressLine1: "Jumeirah, Dubai",
      addressLine2: "",
      active: true,
      userId: "user123"
    }
  ]);
}
```

---
## Image
<img src='./assets/Screenshot 2025-11-20 104742.png'>
<img src='./assets/Screenshot 2025-11-20 104810.png'>
<img src='./assets/Screenshot 2025-11-20 104829.png'>