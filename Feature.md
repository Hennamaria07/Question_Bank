# Add Spare Parts

Create a **single self-contained HTML file** (pure HTML + CSS + vanilla JavaScript only) for the route  
`/app/settings/spareparts/add/:userId` that implements a complete **Add Spare Parts** interface with temporary cart-style behavior using `localStorage` and `sessionStorage`.

---

## Header
- **Back Arrow** (Left Arrow) with **bouncing animation** on hover  
  → Navigates to `/app/settings/spareparts/:userId`  
  → Shows **confirmation dialog** if there are unsaved parts in `sessionStorage.spareParts`
- Page Title: **Add Spare Parts** (24px, bold, #232323)

---

## Layout (Responsive Flexbox)

| Section                | Flex     | Background   | Purpose                                   |
|------------------------|----------|--------------|-------------------------------------------|
| **Left – Form**        | `flex: 3`| `#E5E8FF`    | Spare part input form                     |
| **Right – Preview**    | `flex: 2`| `#E5E8FF`    | Live preview of added parts (cards)       |

- Right section **visible only when parts exist**
- Preview area: scrollable, `max-height: 400px`, custom styled scrollbar (8px width, #888 → #555 hover)

---

## Form Fields (All required – red asterisk *)

| Field            | Type                                 | Validation & Formatting                                                                 |
|------------------|--------------------------------------|------------------------------------------------------------------------------------------|
| Part Name        | Text input                           | Required                                                                                 |
| Part Code        | Text input                           | Required                                                                                 |
| Description      | Text input                           | Required                                                                                 |
| Price            | Number input                         | Regex `/^[0-9]*\.?[0-9]{0,2}$/`<br>• Focus: raw number<br>• Blur: formatted with commas + 2 decimals + currency (AED default) |
| Qty              | Number input (decimal allowed)       | Max 2 decimal places                                                                     |
| Supplier         | Styled `<select>`                    | Populated from `localStorage.suppliers` (only `active: true`)<br>White bg, black text, custom border |
| Exp Date         | Native `<input type="date">`         | Min = today<br>Displayed as `DD-MM-YYYY` (from config or default)                        |

### Form Buttons
| Button   | Style                                      | Action                                      |
|----------|--------------------------------------------|---------------------------------------------|
| Add      | `#91B3FA` bg, `#343434` text, 127×48px     | Validate → add to preview → save to sessionStorage |
| Cancel   | White bg, `#616161` text, border           | Navigate back (with confirmation if unsaved) |

---

## Right Panel – Added Parts Cards

Each card:
- Background: `#F2F2F2`
- Height: 210px, `min-width: 8rem`
- Border: `1px solid #ccc`, `5px` radius
- Padding: 10px, Margin: 10px
- Close Button (Times) top-right → removes item

**Card displays (label: value format):**
- **Part Name** (h5, 18px, bold)
- Part Code
- Description
- Price (formatted with currency)
- Quantity
- Supplier (name looked up from suppliers array)
- Exp Date (DD-MM-YYYY)
- **Total Cost** = Price × Qty (formatted)

---

## Final Save Button (Bottom of preview panel)
- Appears only when ≥1 part added
- Style: `#2A00B2` background, white text, centered
- On click:
  → Validate at least one part exists
  → Show **success toast**
  → Clear `sessionStorage.spareParts`
  → Navigate back to list page

---

## Data Storage

| Storage           | Key               | Content                                                                 |
|-------------------|-------------------|-------------------------------------------------------------------------|
| `localStorage`    | `suppliers`       | Array of `{ id, name, active }` objects                                 |
| `localStorage`    | `config`          | `{ currency: "AED", dateFormat: "DD-MM-YYYY" }`                         |
| `sessionStorage`  | `spareParts`      | Temporary array of added parts (persists on refresh)                    |

**Saved Object Structure:**
```js
{
  name: "Brake Pad",
  partNumber: "BP-2025",
  description: "Front brake pad set",
  price: 250.00,
  quantity: 5.5,
  cost: 1375.00,           // price × quantity
  vendor: "sup_123",
  expiryDate: "2026-12-15",
  active: true
}
```
## Image
<img src='./assets/Screenshot 2025-11-20 121303.png'>