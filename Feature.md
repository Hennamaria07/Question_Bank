# Project Requirement — Collapsible Sidebar Navigation

Create a **single self-contained HTML file** (with CSS and JavaScript embedded inside it) that implements a **fixed collapsible sidebar navigation menu**. The sidebar must meet the following requirements:

## Sidebar Behavior

* The sidebar starts in a **collapsed** state with a width of **5rem**, showing only icons.
* When the user **hovers** over the sidebar or **clicks** it, the sidebar expands to **18rem**.
* The sidebar must remain **fixed** on the left side of the screen.
* When expanded, it should show:

  * A larger version of the logo.
  * A **close button**. Clicking the close button collapses the sidebar.
* The sidebar must **automatically collapse** when the mouse leaves the sidebar area.
* All transitions (opening/closing) should be smooth.
* Submenu items should appear with a **slide-right animation**.

## Design Requirements

* Background color: **#2A00B2** (purple)
* Text color default: **#A3A3A3** (gray)
* On hover, text color changes to **white**.
* Use smooth animations for expanding/collapsing and submenu sliding.
* Use two logo versions: one for collapsed sidebar, one for expanded sidebar.

## Menu Structure

The sidebar contains four main sections:

* **Dashboard**
* **Operations**
* **Settings**
* **Reports**

Each section contains submenu items that must be **hardcoded** and must open **alphabetically sorted** when the parent section is clicked.

### Only one section is allowed to be open at a time.

Clicking on a new section must close the previously opened one.

## Required Submenu Items and URLs

Base URL: `http://127.0.0.1:5500/`

### Dashboard

* Services → `/dashboard/services.html`
* Services Overview → `/dashboard/services-overview.html`
* Approvals → `/dashboard/approvals.html`
* Manual Time Entry → `/dashboard/manual-time-entry.html`

### Operations

* Employee Management → `/operations/employee-management.html`
* Vehicle Management → `/operations/vehicle-management.html`

### Settings

* Holiday Master → `/settings/holiday-master.html`
* Schedule Master → `/settings/schedule-master.html`
* Service Management → `/settings/service-management.html`
* Spareparts Management → `/settings/spareparts-management.html`
* Supplier Management → `/settings/supplier-management.html`
* Inventory → `/settings/inventory.html`

### Reports

* Vehicle Report → `/reports/vehicle-report.html`
* Employee Report → `/reports/employee-report.html`

## Final Output Requirement

Produce the complete working solution as a **single standalone HTML file** that includes:

* Internal **CSS** (no external files)
* Internal **JavaScript** (no external files)
* Hardcoded menu structure
* Fully functional collapsible sidebar with animations as described above.

## Image
<img src='./assets/Screenshot 2025-10-13 132248.png'>
<img src='./assets/Screenshot 2025-10-13 132325.png'>
<img src='./assets/Screenshot 2025-10-13 132347.png'>
<img src='./assets/Screenshot 2025-10-13 132408.png'>
