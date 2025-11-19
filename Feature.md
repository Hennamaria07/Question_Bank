# Payments Management

Create a **single self-contained HTML file** (HTML + inline CSS + inline JavaScript) that implements a complete, responsive, and persistent **Payments Management** interface with real-time calculations, clean purple-themed UI, and full offline functionality.

---

## Header

- Title: **Payments**
  - Font size: **24px**
  - Font weight: **600**
  - Color: `#232323`

---

## Payments Table — Columns

| Column       | Fixed Width | Input Type & Requirements                                                                                                   |
|--------------|-------------|-----------------------------------------------------------------------------------------------------------------------------|
| **Date**     | 160px       | Native `<input type="date">`<br>40px height, 4px border-radius, 2px solid `#D2D5DA`                                    |
| **Description** | 1fr      | Text input (fills remaining space)<br>Same styling as Date input                                                          |
| **Amount**   | 150px       | Right-aligned number input<br>• Regex: `/^\d*\.?\d{0,2}$/`<br>• Strips commas/spaces while typing<br>• Prevents mouse wheel changes<br>• On blur → formats with comma thousands + always 2 decimals<br>• On focus → removes formatting |
| **Action**   | 100px       | Circular buttons with inline SVG icons:<br>• Red **Delete** (trash)<br>• Blue **Add** (+) — **visible only on the last row** |

### Row Behavior
- **Add Row**: Click blue **+** on the last row → appends new empty row
- **Delete Row**: Click red trash → removes row  
  → If only one row remains → clears inputs instead of deleting
- Rows use `data-row-index` attribute + event delegation

---

## Sample Data

- Key: `payments` → array of objects:
  ```js
  [
    { date: "2025-11-19", description: "Initial deposit", amount: 1500.00 },
     { date: "2025-11-19", description: "deposit", amount: 1200.00 }]

## Image
<img src='./assets/Screenshot 2025-11-19 153546.png'>