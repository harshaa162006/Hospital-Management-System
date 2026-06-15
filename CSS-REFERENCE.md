# CSS REFERENCE SHEET
## MediCare Hospital Management System (HMS)

This sheet explains every new layout, dashboard, table, modal, and badge class added to the HMS stylesheet.

---

## 1. SWITCHER & ROLE CLASSES

### `.role-switcher-banner`
* **Purpose**: Sticky header container at the top of the viewport for swapping portals.
* **Key styles**: Dark background (`#0f172a`), bottom border, height `48px`, `position: sticky`, `z-index: 1000`.

### `.role-btn`
* **Purpose**: Buttons inside the role switcher header.
* **Key styles**: Transparent by default, rounded pills (`--radius-full`), blue brand background when `.active` (`var(--clr-primary)`), transitioning on hover.

### `.hms-view`
* **Purpose**: Div containers wrapping Patient, Doctor, and Admin sections.
* **Key styles**: `display: none` by default. Changes to `display: block` and plays slide-up keyframes when given the `.active` class.

---

## 2. DASHBOARD LAYOUT CLASSES

### `.dashboard-layout`
* **Purpose**: Split-screen dashboard template.
* **Key styles**: CSS grid with layout `grid-template-columns: 240px 1fr`, taking full height minus the switcher banner (`calc(100vh - 48px)`).

### `.dashboard-sidebar`
* **Purpose**: Sidebar containing selectors and navigational tab menus.
* **Key styles**: Background `var(--clr-surface)`, solid right border, flexbox alignment of links.

### `.sidebar-link`
* **Purpose**: Navigational anchors in the sidebar.
* **Key styles**: Left-aligned, rounded corners (`--radius-md`), color changes and primary background highlight (`var(--clr-primary-muted)`) when `.active`.

### `.dashboard-content`
* **Purpose**: Scrollable workspace panel to the right of the sidebar.
* **Key styles**: Padding `32px` (`--sp-xl`), auto-scrolling on Y-axis.

---

## 3. TABLES & badgeS

### `.queue-container`
* **Purpose**: Shadowed scroll wrapper around tabular data grids.
* **Key styles**: Border radius `16px` (`--radius-lg`), box shadow (`--shadow-sm`), overflow hidden.

### `.dashboard-table`
* **Purpose**: Standard HMS data grid.
* **Key styles**: Collapsed borders, padding `14px` on table cells, custom hover highlights.

### `.status-badge`
* **Purpose**: Oval indicators for appointments or doctors.
* **Key styles**: Inline flex, rounded pills (`--radius-full`), font-size `11px`, bold.
* **Modifiers**:
  * `.status-badge.pending`: Yellow badge for pending logs.
  * `.status-badge.completed`: Green badge for consulted logs.
  * `.status-badge.cancelled`: Red badge for cancelled logs.

---

## 4. METRICS & SIMULATED CHARTS

### `.metrics-grid`
* **Purpose**: 4-column container for overview metrics.
* **Key styles**: Grid layout utilizing `repeat(auto-fit, minmax(180px, 1fr))` for responsiveness.

### `.metric-card`
* **Purpose**: Overview card detailing a single financial or operational stat.
* **Key styles**: Large typography values (`24px`), small text subtitles (`11px`).

### `.chart-container`
* **Purpose**: Flex row containing CSS simulated chart columns.
* **Key styles**: Height `180px`, flexbox bottom-aligned columns (`align-items: flex-end`).

### `.chart-bar`
* **Purpose**: Gradient column in charts.
* **Key styles**: Gradient fill, height transition of `500ms ease`.

---

## 5. MODALS & PRESCRIPTIONS

### `.modal-overlay`
* **Purpose**: Full-screen backdrop.
* **Key styles**: Blurs background page (`backdrop-filter: blur(4px)`), semi-transparent, `position: fixed`, `z-index: 2000`, active states controlled via `.active` selector.

### `.modal-card`
* **Purpose**: Floating card in modal center.
* **Key styles**: Max width `500px` (or `550px`), rounded `var(--radius-xl)`, shadow `var(--shadow-lg)`.

### `.prescription-card`
* **Purpose**: Printable doctor prescription layout card.
* **Key styles**: Dashed brand border (`1.5px dashed var(--clr-primary-light)`), grid header for hospital info, compact grids for metadata.

### `.med-row-inputs`
* **Purpose**: Input rows inside prescription writer.
* **Key styles**: Grid layout `grid-template-columns: 2fr 1fr 1fr 1fr auto`, aligning medicine inputs and remove actions on a single line.

---
*CSS Reference sheets — MediCare HMS*
