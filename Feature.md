Here is your **clean, structured, production-ready README** for **Q1: Desktop Service Overview (Active Job Cards) – WITHOUT Workers Panel**.

If you want, I can also generate the full `.html` page.

---

# 📘 Service Overview (Active Job Cards) — Desktop Version (≥901px)

This document explains the layout, UI rules, behavior, and mock data for building the **Service Overview (Active Job Cards)** page using **only HTML, CSS, and JavaScript** as a **single self-contained file**.
This version **removes the workers sidebar entirely** and adapts the layout accordingly.

---

## ✅ **1. Page Summary**

A **desktop-only** page (visible at **901px width and above**) showing job cards in a responsive grid. Clicking a card reveals a right-side slide-in panel with full job details.

This page replicates the behavior of the React version **when the workers panel is disabled**.

---

## 🎨 **2. Layout Requirements**

### **2.1 Full Page Layout**

* The page takes **100% viewport width** — no left sidebar.
* Background color: **light grey `#F1F3F7`**.
* Smooth animations (CSS transform + opacity).

### **2.2 Header**

* Full-width bar with dark blue **`#2652E0`** background.
* Centered date with calendar icon.
* Example:
  **🗓 20 November**

---

## 📦 **3. Job Card Grid**

### **3.1 Grid Rules**

* Responsive CSS grid:

  ```css
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  ```
* Typically displays **3–4 cards per row**.
* Gap between cards: **1em**.

### **3.2 Card Style**

* White background
* `border-radius: 12px`
* Padding: `16px`
* Shadow: subtle soft shadow
* On click:
  **`filter: brightness(120%)`**

---

## 🟥 **4. Card Background Color Priority**

The color must strictly follow these rules:

### **Highest Priority**

1️⃣ **Overdue** → Estimated date/time already passed → **Red `#FF0000`**

### **Otherwise based on status**

| Status | Meaning            | Color                |
| ------ | ------------------ | -------------------- |
| 1      | New                | **Yellow `#FFFD00`** |
| 2      | In Progress        | **Green `#7EF782`**  |
| 3      | On Hold            | **Orange `#FF4E00`** |
| 4      | Ready for Delivery | **Blue `#0000FF`**   |
| Other  | Unknown            | **Gray `#808080`**   |

---

## 🏷 **5. Card Content**

Each card displays:

* **Plate Number (bold 20px + car icon)**
* **Estimated delivery date/time**
  Format: `DD-MM-YYYY, 3:30PM`
* **List of active workers**, one per line
  (Hide section if empty)

---

## 📂 **6. Card Click → Slide-In Details Panel**

Clicking a card triggers:

### **6.1 Grid Shrinks**

* Grid animates to **60–65% width**
* Slides left using `transform`

### **6.2 Details Panel (Right Side)**

* Width: **35%**
* Slides in from the right
* Header background: **`#2652E0`**
* Close button: white X on the left
* Content area:

  * Scrollable
  * White background

### **6.3 Panel Displays**

* Plate number
* VIN
* Owner name
* Contact number
* Estimated delivery
* Assigned workers
* Jobs list
* Parts ordered list
* "View Job Card" link
  → Shows `alert("Opening job card...")`

---

## 📱 **7. No Mobile Version**

This file is **desktop only**.
Hide everything above **600px** if needed, but mobile is not required here.

---

## 📚 **8. Dependencies**

* **Font Awesome** (included via CDN)
  Used for icons like car, calendar, close (X).

---

## 🧪 **9. Included Mock Data (16 job cards)**

The file must include the **exact same dataset**:

```js
const jobCards = [
  { id: "1", jobCardNumber: "JC-2025-0001", plateNumber: "ABC 123 GP", vin: "1HGBH41JXMN109186", ownerName: "Thabo Mokoena", contact: "082 555 0192", estimatedDate: "2025-11-18", estimatedTime: "10:00 AM", status: 2, activeWorkers: ["Sipho Zulu", "Lerato Ndlovu"], jobs: ["Oil Change", "Brake Inspection"], parts: [{name: "Oil Filter", qty: 1}, {name: "Engine Oil 5W30", qty: 5}] },
  { id: "2", jobCardNumber: "JC-2025-0002", plateNumber: "XYZ 789 GP", vin: "2HGES16572H599872", ownerName: "Sarah Johnson", contact: "071 234 5678", estimatedDate: "2025-11-20", estimatedTime: "2:30 PM", status: 1, activeWorkers: [], jobs: ["Diagnostics", "AC Service"], parts: [] },
  { id: "3", jobCardNumber: "JC-2025-0003", plateNumber: "ND 456789", vin: "JH4KA9650XC000123", ownerName: "Mike van der Merwe", contact: "083 777 8888", estimatedDate: "2025-11-15", estimatedTime: "11:00 AM", status: 2, activeWorkers: ["James Mthembu"], jobs: ["Suspension Repair"], parts: [{name: "Shock Absorber", qty: 2}] },
  { id: "4", jobCardNumber: "JC-2025-0004", plateNumber: "TAXI 001", vin: "5FNRL38728B401234", ownerName: "David Khumalo", contact: "076 111 2233", estimatedDate: "2025-11-20", estimatedTime: "4:00 PM", status: 4, activeWorkers: ["Peter Dlamini"], jobs: ["Full Service"], parts: [{name: "Air Filter", qty: 1}, {name: "Spark Plugs", qty: 4}] },
  { id: "5", jobCardNumber: "JC-2025-0005", plateNumber: "GP 987 ZZZ", vin: "1FAFP4040YF123456", ownerName: "Nomsa Nkosi", contact: "081 555 1212", estimatedDate: "2025-11-19", estimatedTime: null, status: 3, activeWorkers: [], jobs: ["Waiting for Parts"], parts: [] },
  { id: "6", jobCardNumber: "JC-2025-0006", plateNumber: "BMW 530i", vin: "WBANB3330XCN12345", ownerName: "Dr. Pieter Botha", contact: "082 999 0001", estimatedDate: "2025-11-21", estimatedTime: "9:00 AM", status: 1, activeWorkers: [], jobs: ["Software Update"], parts: [] },
  { id: "7", jobCardNumber: "JC-2025-0007", plateNumber: "CA 123456", vin: "KL1TF56609B123456", ownerName: "Fatima Patel", contact: "072 888 7777", estimatedDate: "2025-11-17", estimatedTime: "3:00 PM", status: 2, activeWorkers: ["Thandi Mokoena", "Sibusiso Ngubane"], jobs: ["Transmission Service"], parts: [{name: "Transmission Fluid", qty: 8}] },
  { id: "8", jobCardNumber: "JC-2025-0008", plateNumber: "JHB 555 GP", vin: "1G1YY22G0W5101234", ownerName: "Lucas Ferreira", contact: "084 555 6666", estimatedDate: "2025-11-20", estimatedTime: "11:30 AM", status: 2, activeWorkers: ["Moses Chabalala"], jobs: ["Wheel Alignment"], parts: [] },
  { id: "9", jobCardNumber: "JC-2025-0009", plateNumber: "NDL 777 NW", vin: "JTEBU5JR0K5678901", ownerName: "Kgomotso Molefe", contact: "079 111 2222", estimatedDate: "2025-11-16", estimatedTime: "1:00 PM", status: 1, activeWorkers: [], jobs: ["Major Service"], parts: [{name: "Timing Belt Kit", qty: 1}] },
  { id: "10", jobCardNumber: "JC-2025-0010", plateNumber: "POLO GP", vin: "WVWZZZ9NZ9Y123456", ownerName: "Zanele Mthethwa", contact: "073 999 8888", estimatedDate: "2025-11-20", estimatedTime: "5:00 PM", status: 4, activeWorkers: ["Gift Mabunda"], jobs: ["Clutch Replacement"], parts: [{name: "Clutch Kit", qty: 1}] },
  { id: "11", jobCardNumber: "JC-2025-0011", plateNumber: "LUX 001 GP", vin: "SALFA2D46BA123456", ownerName: "Mr. Singh", contact: "082 333 4444", estimatedDate: "2025-11-14", estimatedTime: "10:00 AM", status: 2, activeWorkers: ["Isaac Mokoena", "Reggie Phiri"], jobs: ["Engine Overhaul"], parts: [{name: "Head Gasket", qty: 1}, {name: "Pistons", qty: 6}] },
  { id: "12", jobCardNumber: "JC-2025-0012", plateNumber: "TIG 222 FS", vin: "ADTJVN12345678901", ownerName: "Maria da Silva", contact: "081 777 9999", estimatedDate: "2025-11-20", estimatedTime: null, status: 1, activeWorkers: [], jobs: ["Pre-Roadworthy"], parts: [] },
  { id: "13", jobCardNumber: "JC-2025-0013", plateNumber: "FIESTA 1", vin: "3FADP4EJ9KM123456", ownerName: "Tebogo Radebe", contact: "076 444 5555", estimatedDate: "2025-11-19", estimatedTime: "12:00 PM", status: 3, activeWorkers: [], jobs: ["Waiting Approval"], parts: [] },
  { id: "14", jobCardNumber: "JC-2025-0014", plateNumber: "KIA 888 KZN", vin: "KNAFE222695123456", ownerName: "Bongani Zungu", contact: "083 222 3333", estimatedDate: "2025-11-20", estimatedTime: "3:00 PM", status: 2, activeWorkers: ["Lucky Mabaso"], jobs: ["Brake Pads & Discs"], parts: [{name: "Brake Pads Front", qty: 1}, {name: "Brake Discs", qty: 2}] },
  { id: "15", jobCardNumber: "JC-2025-0015", plateNumber: "MERC 63", vin: "WDDHF8JB0EB123456", ownerName: "Ahmed Khan", contact: "082 111 9999", estimatedDate: "2025-11-20", estimatedTime: "10:00 AM", status: 4, activeWorkers: ["Victor Ndlovu"], jobs: ["Service A"], parts: [{name: "Synthetic Oil", qty: 8}] },
  { id: "16", jobCardNumber: "JC-2025-0016", plateNumber: "RANGER GP", vin: "1FTER4FH1KLE12345", ownerName: "Jaco Pretorius", contact: "084 777 8888", estimatedDate: "2025-11-18", estimatedTime: "4:00 PM", status: 2, activeWorkers: ["Themba Mkhize", "Sello Ramaphosa"], jobs: ["Turbo Replacement"], parts: [{name: "Turbocharger", qty: 1}] }
];
```

---
## Image
<img src='./assets/Screenshot 2025-11-20 145245.png'>