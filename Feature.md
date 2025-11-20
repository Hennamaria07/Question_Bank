# README — Login & Password Reset (Single-file HTML)

**Project:** Self-contained Login & Password Reset page
**Files:** Single HTML file (pure HTML, CSS, vanilla JavaScript)
**Author / Style:** Purple-themed, clean layout, centered card design.
**Intended use:** Local/demo environments where credentials and configuration are stored in `localStorage` (no backend).

---

## Overview

This repository contains a single self-contained HTML file that implements a complete **Login** and **Password Reset** UI using only HTML, CSS and JavaScript. All data is stored and read from browser storage (`localStorage` and `sessionStorage`). The UI is centered on-screen, uses a two-column layout (company image left, form right), and includes:

* Toggle to switch between **User** and **Admin** login modes.
* Employee/Admin ID and Password inputs with icons.
* Password visibility toggle.
* Simulated loading state with spinner and disabled inputs.
* Login-by-QR area (configurable).
* On-first-login default-password flow → automatic **Password Reset** screen.
* Responsive behavior for small/medium/large screens.
* All state persisted locally (no APIs).

This README documents usage, expected `localStorage` and `sessionStorage` keys, customization points, and troubleshooting.

---

## How to use

1. Put the single HTML file anywhere and open it in a modern browser (Chrome, Edge, Firefox).
2. Before testing, add required sample data to `localStorage` via the browser console (see *LocalStorage keys & formats* below).
3. Use the Employee ID / Password to sign in. On successful login, session details are saved and the app will check if the stored password is the default (in which case password reset mode is shown).

No server, build step, or dependencies are required.

---

## LocalStorage keys & expected formats

The page expects several keys in `localStorage`. The README provides sample objects to paste in a browser console.

### `config`

Global configuration object. Minimal example:

```js
localStorage.setItem('config', JSON.stringify({
  companyInfo: {
    mainImage: 'data:image/png;base64,...' // or an image URL
  },
  ui: {
    showQrLogin: true,      // boolean — show "Login by QR Code" text/area
    dateFormat: 'DD-MM-YYYY'
  }
}));
```

* `config.companyInfo.mainImage` is used for the left-side clickable image area.
* Any valid image URL or base64 data URI will work.

### `users`

Array of user objects. Example:

```js
localStorage.setItem('users', JSON.stringify([
  {
    id: 'EMP-001',
    role: 'user',            // 'user' or 'admin'
    password: 'password123', // plain-text only for demo purposes (not secure)
    name: 'Aisha Khan',
    defaultPassword: true    // if true, after login the user is forced to reset password
  },
  {
    id: 'ADMIN-01',
    role: 'admin',
    password: 'admin@2025',
    name: 'Admin Person',
    defaultPassword: false
  }
]));
```

> **Important (security):** This demo stores plain-text passwords in `localStorage` for demonstration only. Do not use this in production.

### `session` / `sessionStorage`

On successful login the page will save session details in either `localStorage` or `sessionStorage` depending on implementation (the demo saves to `sessionStorage.sessionUser` for ephemeral sessions):

```js
sessionStorage.setItem('sessionUser', JSON.stringify({
  id: 'EMP-001',
  role: 'user',
  name: 'Aisha Khan',
  loggedAt: '2025-11-20T10:00:00Z'
}));
```

---

## UI & Behavior Details

### Layout & Visual

* Container: white card, centered with `border-radius: 40px`, shadow `0px 8px 4px rgba(0,0,0,0.25)`.
* Two columns:

  * **Left**: displays company logo (from `config.companyInfo.mainImage`), clickable to the homepage (`/` by default). Padding: `68px` vertical and `40px` horizontal (reduced on small screens).
  * **Right**: form area separated by `2px solid #E5E7EB`.

### Login toggle

* Top-right of the form area: toggle switch `50px x 24px`.
* Off (User): gray background; On (Admin): blue `#3a61e0`.
* Round white slider `20px` that moves right when toggled.
* Displays label: `User` or `Admin`.

### Heading

* `Sign In to FIRST CONSULTING GROUP` in uppercase purple text with a slide-right entrance animation.

### Inputs

* Two inputs (or dynamic label):

  * Employee ID / Admin ID (changes with toggle)
  * Password
* Styles:

  * rounded borders `20px` radius
  * background `#F8F8F8`
  * border `1px solid #797979`
  * height `60px`
  * width approx `27rem`
* Right icons:

  * ID field: user icon (decorative)
  * Password field: eye icon to toggle visibility

### Sign In button

* Centered, `200px x 60px`, radius `10px`.
* Default background `#91B3FA`, text bold `1.5rem`, color `#2D2D2D`.
* Hover: purple `#6f42c1` and white text.
* Active (clicked): slightly shrinks (CSS transform).
* On click:

  * Inputs and button disabled
  * Spinner shown
  * Credentials validated against `localStorage.users`
  * On success: session saved. If `defaultPassword` is true → automatically enters **Password Reset** mode.
  * On failure: error alert.

### Password Reset flow

* Form replaced by two inputs:

  * New Password
  * Confirm Password (with eye icon)
* Inputs same style as before.
* Reset button `200px x 60px`:

  * Disabled: gray `#575757`
  * Enabled: blue `#91B3FA`
* Button only enabled when both inputs are non-empty and match.
* On click:

  * Save new password to the matching user object in `localStorage.users`
  * Show success message: `Password changed successfully!`
  * Clear fields and reload page, returning to normal login mode.

### Loading & Disabled States

* During loading (simulated auth), all inputs and buttons are disabled.
* Spinner animation in the sign-in button indicates processing.

### QR Code area

* If `config.ui.showQrLogin === true`, the page displays `Login by QR Code` below the sign-in button.
* The demo does not implement scanning; this is a UI placeholder.

---

## Responsive behavior

* The layout centers using flexbox and the main container height matches `window.innerHeight` dynamically.
* **Small screens (≤480px)**:

  * Left image area hides.
  * Padding reduced for the right area.
  * Input widths and button sizes shrink to fit.
* **Medium screens (481–768px)**:

  * Input widths and button sizes reduce moderately (responsive rem-based scaling).
* **Large screens (>768px)**:

  * Inputs and buttons expand to the designed sizes.

All responsive breakpoints are implemented using CSS media queries inside the single HTML file.

---

## Customization

* **Change company image**: update `config.companyInfo.mainImage` value in `localStorage` (image URL or data URI).
* **Change users**: update `localStorage.users` array.
* **Colors and sizes**: CSS variables are defined near the top of the `<style>` block. Modify variables such as:

  * `--input-bg: #F8F8F8`
  * `--primary-btn: #91B3FA`
  * `--btn-hover: #6f42c1`
  * `--toggle-on: #3a61e0`

---

## Sample setup (paste in browser console)

```js
// config
localStorage.setItem('config', JSON.stringify({
  companyInfo: { mainImage: 'https://via.placeholder.com/300x150?text=Company+Logo' },
  ui: { showQrLogin: true, dateFormat: 'DD-MM-YYYY' }
}));

// users
localStorage.setItem('users', JSON.stringify([
  { id: 'EMP-001', role: 'user', password: 'password123', name: 'Aisha', defaultPassword: true },
  { id: 'EMP-002', role: 'user', password: 'secret', name: 'Suresh', defaultPassword: false },
  { id: 'ADMIN-01', role: 'admin', password: 'admin@2025', name: 'Admin', defaultPassword: false }
]));

// Optional: clear session
sessionStorage.removeItem('sessionUser');
```

Then open the single HTML file and sign in with `EMP-001` / `password123` to test the reset flow.

---
## Image
<img src='./assets/Screenshot 2025-03-28 130604.png'>