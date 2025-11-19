# Manual Time Entry Form — README

## Goal

Create a **single self-contained HTML file** that implements a responsive **Manual Time Entry Form** and will live at:

```
http://127.0.0.1:5500/dashboard/manual-time-entry/manual-time-add.html
```

The form must follow the exact behavior, validation, styling, and persistence rules described below.

---

## Required Fields (read-only)

* **Plate No** (example: `KL-07-AB-1234`) — read-only
* **Brand** (example: `Toyota Camry`) — read-only
* **Job Card Id** (example: `JC-2024-001`) — read-only
* **Advisor Name** (example: `John Smith`) — read-only

## Input Fields (user-editable)

* **Authorized Level** (select dropdown)

  * Sample options: `Sarah Johnson - Level 2`, `Michael Brown - Level 2`, `Emily Davis - Level 2`
* **Task** (select dropdown)

  * Options: `Oil Change`, `Brake Service`, `Engine Repair`, `Tire Rotation`, `Battery Replacement`
* **Start Date** (date picker)
* **End Date** (date picker)

  * Both date pickers default to the current date and must have `min` and `max` set to today's date only (disallow past/future selection).
* **RT Hour** (numeric, 0–10)
* **RT Minutes** (numeric, 0–59)
* **OT Hour** (numeric, 0–24)
* **OT Minutes** (numeric, 0–59)

> Fields marked required must show a red asterisk in their label.

---

## Validation (run on form submission only)

1. If any required field is empty, show toast: **"Please ensure all fields are filled out"**.
2. **End Date** cannot be before **Start Date** — show toast: **"Please ensure the end date is on or after the start date"**.
3. **RT total** (hours + minutes/60) must not exceed **10 hours** — show toast: **"RT hours and minutes cannot exceed 10 hours"**.
4. **Combined RT + OT** (RT decimal + OT decimal) must not exceed **24 hours** — show toast: **"Combined RT and OT hours cannot exceed 24 hours"**.
5. Hour and minute fields must accept only numeric input; prevent non-numeric key presses except Backspace, Delete, Arrow keys, and Tab.

---

## Toast Notification System

* Toasts appear at the **top-right** of the screen with a fade-in animation.
* Auto-dismiss after **3 seconds**.
* Error toasts: white background, dark text `#333333`, padding `16px 24px`, border-radius `8px`, box-shadow for elevation.
* Success toast: green background `#16A34A` with white text and same sizing.

---

## On Successful Submission

1. Display success toast: **"Time entry added successfully"** (green background).
2. Store the entry in `localStorage` under key `manualTimeEntries` as an array of objects. Append new entries to existing array.

   * Each saved object shape:

     ```json
     {
       "plateNo": "...",
       "brand": "...",
       "jobCardId": "...",
       "advisorName": "...",
       "authorizedLevel": "...",
       "task": "...",
       "startDate": "DD-MMM-YYYY",
       "endDate": "DD-MMM-YYYY",
       "rtHour": 1.5, // decimal hours (hours + minutes/60)
       "otHour": 2.25, // decimal hours
       "timestamp": "2025-06-05T12:34:56.789Z"
     }
     ```
3. Log the saved data to the console.
4. Wait **1.5 seconds** after showing success toast, then navigate to:

```
http://127.0.0.1:5500/dashboard/manual-time-entry.html
```

5. If the user clicks **Cancel**, immediately navigate to the same URL without saving.

---

## Styling Requirements

* **Primary button (Save)**: background `#2A00B2`, white text, width `127px`, height `48px`, border-radius `10px`, box-shadow `0px 4px 4px rgba(0,0,0,0.25)`.
* **Cancel button**: white background `#FFFFFF`, gray text `#616161`, same dimensions as Save.
* **Inputs**: white background `#FFFFFF`, text color `#6D7280`, border `1px solid #D2D5DA`, border-radius `6px`, height `42px`, padding `0 12px`.
* **Labels**: font-size `16px`, font-weight `500`. Required labels show red asterisk.
* **Card/container**: background `#E5E8FF`, shadow `0px 4px 4px rgba(0,0,0,0.25)`, border-radius `10px`.
* **Page body**: background `#F1F3F7`.
* **Font family**: `Helvetica, "Helvetica Neue", Arial, sans-serif`.
* **Autofill styling**: preserve white background and text color.
* **Custom selects** styled identically to inputs (height, border, padding).
* **Date inputs** show placeholder `DD-MM-YYYY` and include a calendar icon; styled consistently with inputs.

---

## Layout & Responsiveness

* **Desktop (min-width: 1200px)**: two-column grid; container width `50%`, centered; top margin `130px`; padding `30px`.
* **Tablet (≤ 1200px)**: single column; width `90%`; top margin `30px`.
* **Mobile (≤ 728px)**: single column; full-width form groups.
* **Buttons** (Save + Cancel) centered at bottom with gap between them.

---

## Accessibility & UX Details

* Show inline validation messages via toast only on submission (no live inline errors).
* Prevent entering invalid characters in numeric fields.
* Ensure keyboard accessibility for selects and inputs.

---

## Image
<img src='./assets/Screenshot 2025-11-19 132515.png'>

---
