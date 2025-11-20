# Spare Parts Management

Create a **single self-contained HTML page** (HTML + CSS + vanilla JavaScript) to manage **Spare Parts**. The page reads and writes data to `localStorage.spareParts` and is fully interactive with **search, filter, and pagination**. The design should be modern, clean, and responsive with a purple-themed style.

---

## Navigation & Header

* Page URL: `/app/settings/spareparts/:userId`  
  `:userId` is used for routing the Add/Edit pages.
* Header Section:
  * Back arrow (←) navigates to the previous page
  * Page title: `"Spare Parts Management"`

---

## Toolbar

* Positioned below header
* Left: Search input with placeholder `"Search parts..."` and search icon
* Right: 
  * **Filter** button (with filter icon)
    * Opens a popover/dropdown panel below the button
    * Contains:
      * Seller Name dropdown (options from `localStorage.suppliers`, includes `"All"`)
      * RESET button (clears filters)
      * Close (X) icon
  * **Add** button (with + icon)
    * Navigates to `/app/settings/spareparts/add/:userId`

---

## Table Container

* Card-style container:
  * Background: `#FFFFFF`
  * Border-radius: 15px
  * Box-shadow: subtle
  * Margin: 30px left/right
* Table Columns:
  | Column      | Description |
  |------------|-------------|
  | Part Name  | Name of the part |
  | Part Code  | Unique part code |
  | Description | Part description |
  | Price      | Right-aligned, formatted to 2 decimals, includes currency symbol (e.g., AED) |
  | Qty        | Right-aligned quantity |
  | Seller Name | Vendor or supplier name |
  | Exp Date   | Formatted as DD-MM-YYYY |
  | Status     | Rounded pill: `"Active"` in green (#E8F5E9), `"Inactive"` in red (#FFEBEE) |
  | Actions    | Edit icon (blue pencil) |

* Row Styling:
  * Odd rows: `#F7F6FE`
  * Even rows: `#FFFFFF`
  * No visible borders
* Header Styling:
  * Bold uppercase text
  * Background: `#FFFFFF`
  * Padding: 16px

---

## Filtering & Search

* **Search**:
  * Filters displayed data as the user types
  * Matches Part Name, Part Code, Description (case-insensitive)
* **Filter**:
  * Seller Name dropdown
  * Current filters stored in a JavaScript object
  * Filter applied dynamically on data array
  * RESET button clears filters and restores full data

---

## Pagination

* Client-side pagination at bottom of table
* Controls:
  * Rows per page dropdown: 10 / 20 / 30 / 40
  * "Page X of Y" text
  * Previous / Next arrow buttons
* Implementation:
  * Slice the filtered data array based on current page and rows per page

---

## Actions

* Edit:
  * Clicking pencil icon navigates to `/app/settings/spareparts/edit/:partId`

---

## Data Structure

* LocalStorage key: `spareParts`
* Array of objects with properties:
```js
[
  {
    _id: "SUP001",
    name: "Alpha Traders",
    supplierId: "ALP12345",
    contactNumber: "+971-555123456",
    addressLine1: "123 Main Street",
    addressLine2: "Dubai",
    active: true,
    userId: "USR001"
  },
  {
    _id: "SUP002",
    name: "Beta Supplies",
    supplierId: "BET67890",
    contactNumber: "+971-555987654",
    addressLine1: "456 Industrial Area",
    addressLine2: "Sharjah",
    active: true,
    userId: "USR002"
  },
  {
    _id: "SUP003",
    name: "Gamma Parts",
    supplierId: "GAM11223",
    contactNumber: "+971-555112233",
    addressLine1: "789 Trade Road",
    addressLine2: "Abu Dhabi",
    active: false,
    userId: "USR003"
  }
]

```

---
## Image
<img src='./assets/Screenshot 2025-11-20 110620.png'>
<img src='./assets/Screenshot 2025-11-20 110646.png'>