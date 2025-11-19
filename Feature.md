# Job History Management

Create a **single self-contained HTML file** (HTML + inline CSS + vanilla JavaScript) implementing a **Job History Management Page** that clearly shows a vehicle’s service history. The page must follow a **clean, responsive layout** and provide user-friendly features such as search, filtering, pagination, and PDF generation.

---

## Header

* Top-left **History** title
  * Font size: **24px**
  * Font weight: **bold**
  * Color: `#333333`

---

## Container

* Card-style container:
  * Margin: `0 30px`
  * Padding: `20px`
  * Background: `#E5E8FF`
  * Border-radius: `8px`
  * Box-shadow: `0px 4px 4px rgba(0,0,0,0.25)`

---

## Search and Filter

* **Search Box**
  * Full-width, top-right
  * Matches against Arrival Date, Delivery Date, Total Hours, and Total Amount  

* **Filter Button**
  * Opens small popover (220px width)
  * Allows filtering by **Arrival Date** and **Delivery Date**
  * Includes **RESET** button to clear filters

---

## Job History Table

* Columns:
  * Arrival Date
  * Delivery Date
  * Total Hours (decimal → HH:MM)
  * Total Amount (currency, formatted with commas and 2 decimals)
  * Invoice (PDF button)
* Header styling:
  * Background: `#D0D4F2`
  * Rounded corners
* Row styling:
  * Odd rows: `#F7F6FE`
  * Even rows: `#FFFFFF`
* Currency formatting:
  * Use `Intl.NumberFormat` with locale from config or fallback `"en-US"`
* Date formatting:
  * Display `DD-MM-YYYY` or use format defined in config

---

## PDF Button & Modal

* Clicking PDF icon opens a modal titled **“Select Invoice Date”**
  * Options:
    * Current Date
    * Delivery Date
    * Pick a Date → shows date picker
  * Validates that a date is chosen
  * On confirm → navigate to `/invoice/{jobCardId}` with selected date in route state
* If no date selected → show top-center red toast: **“Please select an invoice date.”**
* Modal behavior:
  * Close on backdrop click
  * Close on Escape key

---

## Pagination

* Server-like pagination:
  * Rows per page: 5, 10, 20
  * Previous / Next navigation
  * Display line: `"Showing X–Y of Z entries"`

---

## Data Handling

* Load data from `localStorage.jobHistory`
* Filter records by `vehicleId`
* Each record includes:
  * Job card info
  * Services
* Compute:
  * **Total Hours** = sum of service actual hours → display as HH:MM
  * **Total Amount** = sum of service actual costs → formatted currency
* Search & filters:
  * Search matches against dates and amounts
  * Date filters match exact Arrival/Delivery Dates
* Display **No history available** if no records exist
* Show **centered loading spinner** while fetching

---

## Accessibility & Styling

* All inputs and controls:
  * Accessible styling
  * `box-sizing: border-box`
* Layout is responsive:
  * Column widths reduce on narrower screens
  * Header padding shrinks
  * Table becomes scrollable

---

## Error Handling

* All localStorage operations wrapped in try/catch
* Show **user-friendly error messages** via toast notifications

---

## Summary of Features

* Bold **History** header
* Card-style container with shadow
* Responsive job history table with alternating row colors
* Full-width search and filter popover
* PDF button with modal to select invoice date
* Pagination with rows per page selection
* Total Hours & Amount calculations
* Loading spinner while fetching data
* Accessible, responsive, and mobile-friendly layout
* Robust error handling and toast notifications


## Image
<img src='./assets/Screenshot 2025-11-19 160950.png'>
<img src='./assets/Screenshot 2025-11-19 161018.png'>
<img src='./assets/Screenshot 2025-11-19 161129.png'>
<img src='./assets/Screenshot 2025-11-19 161155.png'>