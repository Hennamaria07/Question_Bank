# Job Approval — Authorization Page

## Goal

Create a **single-file HTML/CSS/JavaScript** page that implements a **Job Approval Authorization** editor. The page stores everything in `localStorage` and manages multi-level approval hierarchies (Strength → Root Level → Level 2–5). It must be responsive, accessible, robust, and use a purple-accent clean theme.

---

## Top-level UI

* Centered card container with padding, rounded corners, and subtle shadow.
* `h2` title: **Job Approval**.
* Responsive approval rows table with columns:

  * **Strength** (select 0–4)
  * **Root Level** (select from roles list; unique across rows)
  * **Level 2** (select)
  * **Level 3** (select)
  * **Level 4** (select)
  * **Level 5** (select)
  * **Actions** (Delete / Undo / History icons depending on version/state)

Behavior summary:

* Strength controls how many level selects are visible (Strength = 0 shows no extra selects, Strength = 3 shows Level2–4, etc.).
* Reducing Strength clears higher levels automatically.
* Root Level options exclude roles already used as roots in other rows. Selecting a duplicate root triggers an error toast and prevents the selection.
* Within a row, Level selects must exclude roles already chosen in that same row (no duplicate roles within a hierarchy). A helper function `clearDuplicateRoles(row)` removes/clears any duplicated selections.

---

## New-row input & Add behavior

* At the table bottom there is a new-row input line (Strength + Root Level + Level2–5 selects) and a **plus (+) Add button**.
* Clicking the **Add** (plus icon) performs:

  1. **Validation** — Root Level must be selected; enforce no duplicate roles within the new row and no duplicate root across rows.
  2. **Generate ID** — unique id created using timestamp+random or UUID (e.g. `Date.now().toString(36) + '-' + Math.random().toString(36).slice(2,8)`).
  3. **Append Row** — push new object into the `approvalLevels` array in `localStorage` and update the UI.
  4. **Reset** the new-row inputs to defaults.
  5. **Log** action to console and show a success toast.

Client-side function to call on add: `addNewApprovalRow()` — this is bound to the plus icon's `click` event.

---

## Delete / Undo / History actions

* The **Actions** cell contains:

  * **Delete (trash)** icon for v1 rows — clicking it prompts confirmation and then removes the row from the `approvalLevels` array and updates localStorage. If deletion is disallowed (e.g., referential constraint) show a tooltip explaining why.
  * For later versions, show **Undo / History** icons to revert or inspect previous versions.
* The Delete handler is `deleteApprovalRow(id)` — bound to the trash icon `click` event. It logs the action, updates localStorage, and shows success/error toasts.

---

## Save behavior

* A **Save** button validates that root levels are unique across the entire table and that rows meet intra-row uniqueness.
* Save collects only changed/new rows (compare using `hasRowChanged(currentRow, originalRow)`), increments `version` for modified rows, sets `createdAt`/`updatedAt` timestamps, and persists the `approvalLevels` array in `localStorage`.
* After save, the script updates user authorizations:

  1. Read `users` from `localStorage`.
  2. Build sets:

     * `rootRoles = Set(level1 values)
     * `approvalRoles = Set(level2..level5 values)
  3. For each user, if user's role is in `approvalRoles`, ensure the "Approvals" menu is present in their `authorizations` array (map menu name to ID via `authorizations` list). If no longer in `approvalRoles`, remove the Approvals menu from that user's authorizations.
  4. Write updated `users` back to `localStorage`.
* Save logs actions and shows success toast.

---

## LocalStorage Keys

* `roles` — array of role objects: `{ id, name }`.
* `authorizations` — array of menu/authorization objects: `{ id, name }`.
* `users` — array of user objects with `role` and `authorizations` fields.
* `approvalLevels` — array of approval rows persisted as objects:

```js
{
  id: 'unique-id',
  index: 0,                // ordering index
  strength: 3,
  level1: 'roleId',        // Root Level
  level2: 'roleId' | null,
  level3: 'roleId' | null,
  level4: 'roleId' | null,
  level5: 'roleId' | null,
  version: 1,
  createdAt: 'ISO timestamp',
  updatedAt: 'ISO timestamp'
}
```

All reads/writes use `JSON.parse()` / `JSON.stringify()` in `try/catch`.

---

## Helper Functions (recommended names)

* `loadData()` — loads roles, users, authorizations, and approvalLevels from `localStorage`.
* `renderTable()` — renders current `approvalLevels` array into the DOM.
* `getAvailableRootLevelRoles()` — returns `roles` minus any `level1` already used.
* `getAvailableRoles(currentRow)` — returns `roles` minus selections already present in `currentRow`.
* `clearDuplicateRoles(row)` — removes duplicate role ids within a single row.
* `hasRowChanged(currentRow, originalRow)` — deep-compare to detect changes.
* `addNewApprovalRow()` — validates and appends a new row (wired to the plus icon `click`).
* `deleteApprovalRow(id)` — deletes a row after confirmation (wired to trash icon `click`).
* `saveApprovalLevels()` — validates and persists changed/new rows and updates users/authorizations.
* `showToast(message, type)` — top-center green/red auto-dismiss toast.

---

## UI Rules & UX

* Duplicate checks:

  * Root Level duplicates across rows → **disallow** and show an error toast.
  * Duplicate roles inside the same row → **clear** the duplicates or prevent selection and show a toast.
* Strength changes clear higher levels automatically.
* Tooltips explain disabled actions (e.g., "Cannot delete — role referenced by X").
* All interactive events should `console.log()` useful debug info (e.g., "Added approval row: {id}", "Deleted approval row: {id}").

---

## Responsiveness

* Desktop: full table with header visible.
* Below breakpoint(s): rows render as stacked card blocks; headers hidden; select controls become full-width; Save/Add buttons become full-width.
* Use data-label pseudo-elements for stacked layout so each field shows a label in compact mode.

---

## Accessibility & Robustness

* Use semantic elements and labels for selects.
* Keyboard accessibility for selects and action icons.
* Use `aria-live` for toasts.
* All localStorage interactions are wrapped in `try/catch` with graceful fallbacks and error toasts.

---

## Add/Delete JavaScript Bindings (explicit)

* The plus icon **MUST** have an onclick bound to `addNewApprovalRow()` so clicking it appends a validated new row.
* Each trash/delete icon **MUST** have an onclick bound to `deleteApprovalRow(id)` so clicking it removes the row (after confirmation) and updates `localStorage`.

---

## Output

Produce a **single self-contained HTML file** that implements the above behaviors and persists all data in `localStorage`.

---
## Image
<img src='./assets/Screenshot 2025-07-22 102612.png'>