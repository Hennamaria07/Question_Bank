# Invoice Preview — README

## Goal

Create a **single self-contained HTML file** (HTML + inline CSS + vanilla JavaScript) implementing a **complete Invoice Preview Page**. The page must follow a **clean purple-accent theme**, remain fully responsive across desktop, mid-width, and mobile layouts, and support printing, PDF download, and sharing via WhatsApp.

---

## Header

* Top-left **Back Arrow Button**  
  * Hidden when viewing a shared invoice URL  
* Heading area with page title (optional per design)  

---

## Invoice Box — Overview

A **centered invoice container** (max-width 920px) containing:

1. **Company Header Image**
   * From `localStorage.config.companyInfo.invoiceHeader`  
   * Fallback to default logo if missing  

2. **Invoice Title**
   * Bold, centered: **TAX INVOICE**  
   * Display **Job Card Number** and **Invoice Date**  

3. **Customer Section**
   * Pull details from `localStorage.jobCards`, `localStorage.vehicles`, and `config`  
   * Fields include:
     * Name, Contact, Address  
     * Plate Number, Kilometers  
     * Brand/Model, VIN  
     * Emirates, TRN  
     * Insurance/Claim/LPO Numbers  

---

## Spare Parts Table

| Column         | Description |
| -------------- | ----------- |
| S.No           | Serial number |
| Part Description | Part name/description |
| Unit Price     | Price per unit |
| Qty            | Quantity |
| Amount         | Unit × Qty |
| Discount       | Discount amount |
| Gross Amount   | Amount − Discount |
| VAT 5%         | Gross × 0.05 |
| Net Amount     | Gross + VAT |

* Data filtered by `jobCardId` from `localStorage.parts`  
* Calculations performed in JS with **Intl.NumberFormat** (fallback `"en-US"`)  
* Currency values formatted to two decimals  

---

## Services Table

| Column         | Description |
| -------------- | ----------- |
| S.No           | Serial number |
| Work Description | Service description |
| Unit Price     | Price per unit |
| Qty            | Quantity |
| Amount         | Unit × Qty |
| Discount       | Discount amount |
| Gross          | Amount − Discount |
| VAT 5%         | Always 0.00 for services |
| Net            | Gross + VAT |

* Data from `jobCards[].services` filtered by current job card  
* Calculations handled similarly to spare parts table  

---

## Totals Section

* **Parts Subtotal**  
* **Services Subtotal**  
* **Footer Totals**:
  * Total AED  
  * Discount AED  
  * Gross Total  
  * VAT 5% (for parts only)  
  * Net Amount  

---

## Payments Summary

* Paid Amount: Sum of `localStorage.payments` filtered by jobCardId  
* Balance: Net − Paid  

---

## Signature Lines

* Customer  
* Service Advisor  

*Centered "THANK YOU" message beneath signatures*

---

## Action Buttons

1. **Print** → calls `window.print()`  
2. **Download** → generates PDF of invoice area  
3. **Share** → opens WhatsApp share link to invoice view URL  

*Hide Print/Share buttons when viewing a shared invoice.*

---

## Responsiveness

* On narrow screens: tables scroll horizontally, layout stacks  
* Show **“← Scroll to see more →”** hint under 1000px width  
* Adjust fonts/padding across breakpoints  

---

## Print View

* Hide UI controls and buttons  
* Optimize invoice layout for paper  

---

## Data Handling

* Load data from `localStorage`:
  * `config`  
  * `jobCards`  
  * `vehicles`  
  * `parts`  
  * `services`  
  * `payments`  
* Fallback defaults if data is missing (empty string or 0.00)  
* Format dates as `YYYY-MM-DD` (or `config` format if present)  
* Generate unique IDs using `Date.now()+Math.random()` if needed  
* Format all currency consistently  

---

## Error Handling

* Catch errors when accessing localStorage  
* Show friendly error message with **“Go Back”** button  

---

## Loading State

* Display **centered spinner** while fetching data  

---

## Calculations

* **Gross, VAT, Net, Totals, Paid, Balance** calculated in JavaScript  
* Clear, human-readable formatting  

---

## Output

Produce a **single self-contained HTML file** that includes:

* Header with back button  
* Centered invoice box with logo, title, job card info, and customer details  
* Spare parts table and services table with dynamic calculations  
* Totals section and payments summary  
* Signature lines and “THANK YOU” message  
* Action buttons for Print, Download, Share  
* Responsive layout and print-friendly view  
* Loading spinner and error handling  


## Image
<img src='./assets/Screenshot 2025-11-19 155833.png'>
<img src='./assets/Screenshot 2025-11-19 155852.png'>
<img src='./assets/Screenshot 2025-11-19 155913.png'>