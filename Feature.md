# Task Overview Page - Requirements (README)

## Overview

This document describes the complete requirements for building a **Task Overview Page** using a **single self-contained HTML file (HTML + CSS + JavaScript)**. The page must be designed for **desktop screens**, with a clean, modern UI using a **light gray background**, **white card-based table**, **smooth transitions**, and a **purple theme**.

The final page must be accessible at:

```
http://127.0.0.1:5500/dashboard/services.html
```

---

## Functional Requirements

### 1. Display Job Orders Table

* Show **15 sample job orders** with the following fields:

  * Plate Number
  * Brand
  * Job Card ID
  * Estimated Delivery Date
  * Advisor Name
* Use a **white card-style table** centered on the screen.
* **Alternating row colors** and **smooth hover highlight effect**.
* One job order — `JC-2024-002` — must be **highlighted in light green** to indicate the active session.
* Clicking any row should redirect to:

```
http://127.0.0.1:5500/dashboard/task/startservice.html
```

---

## 2. Toolbar (Above the Table)

The toolbar must contain:

### **A. Search Bar (Left Side)**

* Filters the table **in real time** as the user types.
* Searchable fields:

  * Plate Number
  * Brand
  * Job Card ID
  * Advisor Name

### **B. Two Dropdown Filters**

* **Brand Filter**
* **Advisor Filter**
* Both filters can work **independently or together** with the search bar.

### **C. Action Buttons (Right Side)**

#### **1. Rejection Button**

* Blue color when rejections exist, light blue when none.
* Shows a red badge with number of rejections → **3**.
* On click, open:

```
http://127.0.0.1:5500/dashboard/rejection.html
```

#### **2. QR Scanner Button**

* Gray button that turns blue on hover.
* On click → `alert("QR Scanner clicked")`

#### **3. Day End Task Button**

* Green when an active session exists.
* Gray when no active session.
* Tooltip: **"Day End Task"**

##### When clicked (if green):

1. Show a confirmation dialog:
   **“Do you want to end the day task?”**
2. If Yes → show a second dialog:

   * Ask: **“Did you work during break time?”**
   * Two input fields:

     * Hours
     * Minutes
3. Validation:

   * If both are `0` or empty → show red toast:
     **“Please enter valid worked hours or minutes.”**
4. If valid time provided → show confirmation alert.
5. If first dialog = No → show:
   **“Break time skipped.”**

---

## 3. Pagination Controls

* Appears below the table.
* Must include:

  * Rows per page dropdown (10, 25, 50)
  * Previous button
  * Next button
  * Page numbers

---

## Style & Layout Requirements

* Clean, modern UI.
* Light gray background.
* White table card with shadow.
* Smooth transitions on hover.
* **Helvetica font** throughout.
* Purple theme accents.
* Table centered on large screens.

---

## Technical Requirements

* Entire project must be a **single HTML file** containing all:

  * HTML structure
  * CSS styling (inside `<style>` tag)
  * JavaScript logic (inside `<script>` tag)
* Must function on desktop browsers.

---

## Sample Data

```js
const jobOrders = [
  { plateNo: "KL-07-AB-1234", brand: "Toyota", jobCardId: "JC1001", estDelivery: "05-Jun-2025", advisor: "Anees" },
  { plateNo: "KL-08-CD-5678", brand: "Honda", jobCardId: "JC1002", estDelivery: "10-Jun-2025", advisor: "Ramesh" },
  { plateNo: "KL-10-EF-9012", brand: "Ford", jobCardId: "JC1003", estDelivery: "12-Jun-2025", advisor: "Kiran" },
  { plateNo: "KL-11-GH-3456", brand: "BMW", jobCardId: "JC1004", estDelivery: "15-Jun-2025", advisor: "Anees" },
  { plateNo: "KL-12-IJ-7890", brand: "Mercedes", jobCardId: "JC1005", estDelivery: "18-Jun-2025", advisor: "Ramesh" },
  { plateNo: "KL-13-KL-1122", brand: "Toyota", jobCardId: "JC1006", estDelivery: "20-Jun-2025", advisor: "Joseph" },
  { plateNo: "KL-14-MN-3344", brand: "Honda", jobCardId: "JC1007", estDelivery: "22-Jun-2025", advisor: "Kiran" },
  { plateNo: "KL-15-OP-5566", brand: "Ford", jobCardId: "JC1008", estDelivery: "25-Jun-2025", advisor: "Anees" },
  { plateNo: "KL-16-QR-7788", brand: "BMW", jobCardId: "JC1009", estDelivery: "28-Jun-2025", advisor: "Ramesh" },
  { plateNo: "KL-17-ST-9900", brand: "Mercedes", jobCardId: "JC1010", estDelivery: "30-Jun-2025", advisor: "Joseph" },
  { plateNo: "KL-18-UA-1111", brand: "Toyota", jobCardId: "JC1011", estDelivery: "02-Jul-2025", advisor: "Anees" },
  { plateNo: "KL-19-VB-2222", brand: "Honda", jobCardId: "JC1012", estDelivery: "05-Jul-2025", advisor: "Ramesh" },
  { plateNo: "KL-20-WC-3333", brand: "Ford", jobCardId: "JC1013", estDelivery: "07-Jul-2025", advisor: "Kiran" },
  { plateNo: "KL-21-XD-4444", brand: "BMW", jobCardId: "JC1014", estDelivery: "10-Jul-2025", advisor: "Joseph" },
  { plateNo: "KL-22-YE-5555", brand: "Mercedes", jobCardId: "JC1015", estDelivery: "12-Jul-2025", advisor: "Anees" },
  { plateNo: "KL-23-ZF-6666", brand: "Toyota", jobCardId: "JC1016", estDelivery: "15-Jul-2025", advisor: "Kiran" },
  { plateNo: "KL-24-AG-7777", brand: "Honda", jobCardId: "JC1017", estDelivery: "17-Jul-2025", advisor: "Ramesh" },
  { plateNo: "KL-25-BH-8888", brand: "Ford", jobCardId: "JC1018", estDelivery: "20-Jul-2025", advisor: "Joseph" },
  { plateNo: "KL-26-CI-9999", brand: "BMW", jobCardId: "JC1019", estDelivery: "22-Jul-2025", advisor: "Anees" },
  { plateNo: "KL-27-DJ-1010", brand: "Mercedes", jobCardId: "JC1020", estDelivery: "25-Jul-2025", advisor: "Kiran" },
  { plateNo: "KL-28-EK-2020", brand: "Toyota", jobCardId: "JC1021", estDelivery: "27-Jul-2025", advisor: "Joseph" },
  { plateNo: "KL-29-FL-3030", brand: "Honda", jobCardId: "JC1022", estDelivery: "30-Jul-2025", advisor: "Anees" },
  { plateNo: "KL-30-GM-4040", brand: "Ford", jobCardId: "JC1023", estDelivery: "01-Aug-2025", advisor: "Ramesh" },
  { plateNo: "KL-31-HN-5050", brand: "BMW", jobCardId: "JC1024", estDelivery: "03-Aug-2025", advisor: "Kiran" },
  { plateNo: "KL-32-IO-6060", brand: "Mercedes", jobCardId: "JC1025", estDelivery: "05-Aug-2025", advisor: "Joseph" }
];
```
## Image
<img src='./assets/Screenshot 2025-11-19 133722.png'>
<img src='./assets/Screenshot 2025-11-19 133741.png'>
<img src='./assets/Screenshot 2025-11-19 133827.png'>