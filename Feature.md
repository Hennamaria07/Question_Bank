# Service Overview — Workers List Card

## Goal

Build a responsive **Service Overview workers list card** (single self-contained HTML/CSS/JS component) that displays workers grouped by role and supports filtering, localStorage persistence, and responsive behavior.

This README describes the UI, functionality, data persistence, and layout requirements so you can implement the component from scratch.

---

## UI & Layout Requirements

* The workers list card is a self-contained component styled with a **purple theme** and clean layout.
* The container sizing:

  * **Desktop (min-width: 1200px):** width **25%** of the viewport, height **98%**, rounded corners, light box shadow.
  * **Tablet (max-width: 1200px):** width **90%**.
  * **Mobile (max-width: 900px):** width **100%** (but hidden by default; see behavior below).
* Font family: `Helvetica, "Helvetica Neue", Arial, sans-serif`.
* Use slightly reduced font sizes on smaller screens for readability.
* The card should show a loading animation for **2 seconds** on initial load before rendering the data.

---

## Data & Structure

* Workers are grouped by **role** (e.g., **Mechanic**, **Technician**). Each role appears as a bold heading, followed by a list of worker entries.
* Each worker entry shows:

  * **Name** (e.g., "Anees K")
  * **Status** badge text: either **Working** (blue) or **Available** (green)
* Example data structure (JS):

```js
const workers = [
  { id: 1, name: 'Anees K', role: 'Mechanic', status: 'Available' },
  { id: 2, name: 'Ramesh P', role: 'Mechanic', status: 'Working' },
  { id: 3, name: 'Kiran S', role: 'Technician', status: 'Available' },
  // ... more workers
];
```

* The app must load initial worker data from `localStorage` if present; otherwise use the hardcoded default dataset. Any updates (e.g., via the Available Workers toggle) must be written back to `localStorage` so state persists across reloads.

---

## Behavior & Interactions

1. **Loading state**

   * On page/component load display a lightweight loading animation (spinner or shimmer) for 2 seconds, then show the card content.

2. **Grouping & Display**

   * Group workers by `role`. Roles are displayed in bold with the worker list underneath.
   * For each worker, show the name and a colored status label:

     * `Working` → blue label (e.g., `#2563EB`)
     * `Available` → green label (e.g., `#10B981`)

3. **Available Workers Toggle**

   * Include a toggle switch labeled **"Available Workers"** at the top of the card.
   * When toggled **on**, filter the view to show only workers whose status is `Available`.
   * When toggled **off**, show all workers grouped by role.
   * Toggling must update and persist the filter state in `localStorage` so the same view is restored after reload.

4. **Mobile Behavior**

   * On **mobile devices**, the workers list card is **hidden by default**.
   * Provide a **dropdown menu** or select control elsewhere on the page (or at the top) that allows the user to show/hide the workers card. Selecting the workers view should display the card (covering or sliding into the viewport as appropriate for your layout).

5. **Empty State**

   * If the worker list is empty (after filtering or because no data exists), display a centered fallback message:

     * **"No workers found"**
   * Style the fallback message clearly and centered inside the card.

6. **Persisting Changes**

   * Any interaction that changes the displayed list (such as toggling the Available-only switch) must update `localStorage` to persist the filter state and any worker status changes.

---

## Accessibility & UX

* Make the toggle keyboard accessible (focusable and operable with Space/Enter).
* Ensure color-contrast for status badges and text meets reasonable accessibility.
* Provide proper `aria` attributes for dynamic elements (e.g., `aria-pressed`, `aria-live` for the empty state message if needed).

---

## Sample Implementation Notes

* Use semantic markup: `<section>` for the card, headings for roles, `<ul>/<li>` for worker lists.
* Keep JavaScript modular: functions for `loadData()`, `render()`, `applyFilter()`, `saveState()`.
* Use CSS transitions for show/hide and for the loading animation fade.

---

## Example Default Dataset (you can extend as needed)

```js
{
  "workers": [
    {
      "id": 1,
      "name": "Arjun Kumar",
      "role": "Mechanic",
      "status": "Working"
    },
    {
      "id": 2,
      "name": "Rahul Sharma",
      "role": "Mechanic",
      "status": "Available"
    },
    {
      "id": 3,
      "name": "Vikram Singh",
      "role": "Mechanic",
      "status": "Working"
    },
    {
      "id": 4,
      "name": "Suresh Nair",
      "role": "Mechanic",
      "status": "Available"
    },

    {
      "id": 5,
      "name": "Imran Ali",
      "role": "Technician",
      "status": "Working"
    },
    {
      "id": 6,
      "name": "Deepak Verma",
      "role": "Technician",
      "status": "Available"
    },
    {
      "id": 7,
      "name": "Mohammed Faisal",
      "role": "Technician",
      "status": "Available"
    },
    {
      "id": 8,
      "name": "Ramesh Patel",
      "role": "Technician",
      "status": "Working"
    },

    {
      "id": 9,
      "name": "Samuel D’Souza",
      "role": "Electrician",
      "status": "Available"
    },
    {
      "id": 10,
      "name": "Karthik R",
      "role": "Electrician",
      "status": "Working"
    },

    {
      "id": 11,
      "name": "Roshan Jacob",
      "role": "Painter",
      "status": "Available"
    },
    {
      "id": 12,
      "name": "Naveen Kumar",
      "role": "Painter",
      "status": "Working"
    }
  ]
}

```

---

## Output

Deliver a single self-contained HTML file with inline CSS and JavaScript implementing the above behavior. Optionally include a small demo button on the page to reset `localStorage` to the default dataset for testing.

---

## Image
<img src='./assets/Screenshot 2025-11-19 135725.png'>
<img src='./assets/Screenshot 2025-11-19 135733.png'>