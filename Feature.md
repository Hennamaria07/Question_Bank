# Master Configuration

Create a **single self-contained HTML file** (HTML + CSS + JavaScript) implementing a **Master Configuration Add Form** for storing company settings in `localStorage`. This page is **for adding new configuration only** (no edit/update functionality). The UI should be **clean, responsive, and user-friendly** with proper validations, file handling, and state management.

---

## Container & Layout

* Card-style container:
  * Background: `#E5E8FF`
  * Padding: `20px`
  * Rounded corners
  * Soft shadow
* Form layout:
  * Responsive grid
  * Auto-fit columns with **min-width: 300px**
  * Collapses to **single-column stack** below 1200px

---

## Sections & Inputs

### 1. Company Information

* Fields:
  * Client Code
  * Client Name
  * Email
  * Website
  * TRN
  * Address (textarea)
* Phone/Fax groups:
  * Two groups
  * Country-code select + phone input
  * Phone input accepts **digits only** and validates length
* Color / Custom Fields:
  * Custom 1 default: `#2A00B2`
  * Custom 2
  * Face Unlock timeout default: `5000ms`
* File inputs:
  * Sidebar logo
  * Sidebar open logo
  * Login image
  * Invoice header
  * **Validations**:
    * File type: PNG/JPG
    * Max pixel dimensions
  * Show **preview URLs** if images exist

---

### 2. Module Configuration

* Checkbox tiles for features:
  * Time Management
  * Vehicle Management
  * Inventory
  * Face Unlock
  * Enable Add Job Card Service/Part
* **Dependencies**:
  * Enabling Time Management automatically enables Vehicle Management and Quotation
  * Quotation must remain enabled

---

### 3. Globalisation

* Styled selects for:
  * Date Format (e.g., DD-MM-YYYY, YYYY-MM-DD)
  * Number Format (e.g., lakh en-IN, million en-US)

---

## Example Mock Data

For testing the "Add New" form, the page can initialize `localStorage.masterConfig` as an empty array:

```js
// Initialize empty config array if missing
if (!localStorage.masterConfig) {
  localStorage.masterConfig = JSON.stringify([]);
}

// Example new entry object after filling form:
{
  _id: Date.now() + Math.random(),
  companyInfo: {
    clientCode: "CL001",
    clientName: "First Consulting Group",
    email: "info@fcg.com",
    website: "https://www.fcg.com",
    TRN: "100234567800003",
    address: "123 Business Bay, Dubai, UAE",
    tel1: { countryCode: "+971", number: "501234567" },
    tel2: { countryCode: "+971", number: "502345678" },
    fax1: { countryCode: "+971", number: "43001234" },
    fax2: { countryCode: "+971", number: "43005678" },
    custom1: "#2A00B2",
    custom2: "#FF5733",
    faceUnlockTimeout: 5000
  },
  moduleConfiguration: {
    timeManagement: true,
    vehicleManagement: true,
    inventory: true,
    faceUnlock: true,
    addJobCardServicePart: true,
    quotation: true
  },
  globalisation: {
    dateFormat: "DD-MM-YYYY",
    numberFormat: "en-IN" // lakh format
  },
  headerImage1: "https://via.placeholder.com/100x50.png?text=Sidebar+Logo",
  headerImage2: "https://via.placeholder.com/100x50.png?text=Sidebar+Open+Logo",
  invoiceHeader: "https://via.placeholder.com/300x100.png?text=Invoice+Header",
  mainImage: "https://via.placeholder.com/200x100.png?text=Login+Image"
}
```
---

## Image
<img src='./assets/Screenshot 2025-11-20 103610.png'>
<img src='./assets/Screenshot 2025-11-20 103632.png'>