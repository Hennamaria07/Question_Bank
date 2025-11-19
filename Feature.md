# Project Description

Create a collapsible sidebar navigation menu using a single self-contained HTML file (with embedded CSS and JavaScript). The sidebar must:

* Start collapsed at **5rem** width showing only icons.
* Expand to **18rem** width when hovered or clicked.
* Be **fixed** on the left side of the page.
* Use purple background **#2A00B2**.
* Include a logo that switches between collapsed and expanded versions.
* Support smooth transitions and slide-right animations.
* Contain 4 parent sections: **Dashboard, Operations, Settings, Reports**.
* Each parent must have submenu items that:

  * Display alphabetically when the parent is clicked.
  * Show hover effects (text color changes from gray **#A3A3A3** to white).
  * Use static hardcoded data.
* Only one parent section may be active at a time.
* A close button must appear when expanded.
* Sidebar must collapse when the mouse leaves or the close button is clicked.

## Required Static Menu Structure & URLs

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

## Output Requirement

Produce the entire solution as a **single standalone HTML file** containing:

* Internal CSS
* Internal JavaScript
* Hardcoded menu data
* Complete working collapsible sidebar as described above.

## Image
<img />