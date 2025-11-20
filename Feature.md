# Mobile Suppliers Management

Create a **single self-contained HTML file** (HTML + inline CSS + vanilla JavaScript) implementing a **Mobile-Optimized Suppliers Management View** for screens under 600px. The page manages supplier data stored in `localStorage` and provides a clean, responsive, and interactive interface.

---

## Container

* Full-height container:
  * Padding: `16px`
  * Background: `#F1F3F7`
* All content scrollable within the container

---

## Toolbar

* Top-right **Filter Button**:
  * Round icon
  * Opens **mobile filter popover** (320px wide)
  * Locks background scrolling when open
* Top-right **Add Button**:
  * Navigates to `/app/settings/suppliers/add/{userId}.html`
  * `userId` derived from the URL

---

## Search Box

* Full-width input:
  * Height: `40px`
  * Padding: `0 12px 0 40px`
  * Border: `2px solid #D2D5DA`
  * Placeholder: `"Search suppliers..."`
* Filters suppliers **as you type** (name, ID, address, contact)
* Resets page to 1 on search change

---

## Supplier Cards

* Stacked white cards:
  * Rounded corners: `8px`
  * Shadow applied
  * Padding: `16px`
* Each card displays:
  * Supplier Name + **Edit Icon** (navigates to `/app/settings/suppliers/edit/{_id}.html`)
  * Supplier ID
  * Status chip: `"Active"` (green) / `"Inactive"` (red)
  * Content block: Address Line 1, Address Line 2, Contact Number
    * Shows `"N/A"` if data missing
* Empty state card when no results:
  * `"No records found / Try adjusting your search or filter criteria"`

---

## Filter Popover

* Width: 320px
* Contains:
  * Select controls for Supplier Name and Supplier ID
    * Options populated from `localStorage.suppliers`
  * RESET button:
    * Clears filters
    * Resets page to 1
* Background scroll locked while popover open
* Closing restores scroll

---

## Pagination

* Fixed bottom bar (always visible)
* Circular page buttons + Previous/Next arrows
* Uses `rows-per-page` to compute total pages
* Bottom padding in content ensures cards are not hidden behind the pagination bar

---

## Data Handling

* Initialize `localStorage.suppliers` if missing
* Fetch `config` if present
* Derive `userId` from URL
* Maintain **state variables**:
  * `data` — current paginated & filtered suppliers
  * `fullSuppliers` — full list for filter dropdown
  * `searchQuery`
  * `filters`
  * `page`
  * `rowsPerPage`
  * `totalCount`
* Data access:
  * Use `JSON.parse` / `JSON.stringify` with `try/catch`
  * Fallbacks to empty arrays to prevent UI crashes
* Supplier object schema:
```js
{
  _id,
  name,
  supplierId,
  contactNumber,
  addressLine1,
  addressLine2,
  active,
  userId,
  createdAt,
  updatedAt
}
```
* Supplier sample data:
```js
[
  {
    _id: "SUP001",
    name: "Alpha Supplies",
    supplierId: "A123",
    contactNumber: "+971501234567",
    addressLine1: "123 Main Street",
    addressLine2: "Warehouse 5",
    active: true,
    userId: "USER001",
    createdAt: "2025-11-01T10:00:00Z",
    updatedAt: "2025-11-10T15:30:00Z"
  },
  {
    _id: "SUP002",
    name: "Beta Traders",
    supplierId: "B456",
    contactNumber: "+971502345678",
    addressLine1: "456 Industrial Rd",
    addressLine2: "",
    active: false,
    userId: "USER001",
    createdAt: "2025-11-05T09:15:00Z",
    updatedAt: "2025-11-12T11:45:00Z"
  },
  {
    _id: "SUP003",
    name: "Gamma Co.",
    supplierId: "G789",
    contactNumber: "",
    addressLine1: "789 Market St",
    addressLine2: "Suite 101",
    active: true,
    userId: "USER001",
    createdAt: "2025-11-08T14:20:00Z",
    updatedAt: "2025-11-15T16:00:00Z"
  }
]
```



## Image
<img src='./assets/Screenshot 2025-11-20 102330.png'>
<img src='./assets/Screenshot 2025-11-20 102347.png'>
<img src='./assets/Screenshot 2025-11-20 102416.png'>