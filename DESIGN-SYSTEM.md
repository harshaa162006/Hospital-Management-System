# DESIGN SYSTEM
## MediCare Hospital Management System (HMS)

This document defines the visual language, design tokens, layout strategies, and components added to support the multi-dashboard Hospital Management System.

---

## 1. BRAND IDENTITY & THEME

* **Hospital Name**: **MediCare Hospital Central Command**
* **Primary Brand Colors**: Deep medical blue (`#1a56db`) representing trust and professional reliability.
* **Secondary Brand Colors**: Emerald green (`#059669`) for positive health outcomes, ratings, and successful financial checkout operations.
* **Neutral Palette**: Clean background tints (`#f8fafc` in light mode, `#0b1120` in dark mode) paired with contrasting surfaces for workspace divisions.

---

## 2. COLOR SYSTEM (HMS ADDITIONS)

In addition to the base booking wizard colors, the following styling colors are used:

### Dark Theme Command Accent
```css
#0f172a — Switcher Background  ████████ Near black sticky role selection panel
#1e293b — Switcher Borders     ████████ Subtle division line for sticky switcher
#60a5fa — Switcher Blue Link   ████████ Neon blue highlight text for logo accent
```

### Dashboard Badges & Statuses
```css
Pending status:   Bg: #fef3c7 (Warning Light)  Text: #d97706 (Warning Amber)
Completed status: Bg: #d1fae5 (Success Light)  Text: #059669 (Success Green)
Cancelled status: Bg: #fee2e2 (Danger Light)   Text: #dc2626 (Danger Red)
```

---

## 3. TYPOGRAPHY & TYPE SCALE

* **Header logotypes**: `Instrument Serif` is used for clinical dashboard brand markings, providing high-end editorial authority.
* **Interface typography**: `DM Sans` is used across all sidebars, tables, and modal grids.
* **Monospace data numbers**: Reference booking numbers (`MC-XXXXXX`) use system monospace fonts to imply precise automated generation.

---

## 4. HMS LAYOUT STRATEGY (SIDEBARS & GRID)

The Doctor and Admin consoles implement a modern split-panel layout:
```
┌─────────────────────────────────────────────────────────┐
│ Sticky Role Switcher Banner                             │
├───────────────┬─────────────────────────────────────────┤
│               │ Dashboard Header                        │
│ Dashboard     ├─────────────────────────────────────────┤
│ Sidebar       │                                         │
│               │ Content Workspace Area                  │
│ • Tab Link 1  │ • Analytics Metrics Grid                │
│ • Tab Link 2  │ • Master Booking Queue Tables           │
│               │ • CSS Bar Charts                        │
│               │                                         │
└───────────────┴─────────────────────────────────────────┘
```

* **Sidebar panel**: Fixed at `240px` width on desktop. Disappears into a top/bottom block on screens under `768px`.
* **Content Area**: Fluid width, utilizing grid-gap spacing scales of `16px` (`--sp-md`) and `24px` (`--sp-lg`).

---

## 5. HMS COMPONENT DESCRIPTIONS

### 📊 Metric Cards
* **Border**: `1px solid var(--clr-border)`.
* **Border Radius**: `16px` (`--radius-lg`).
* **Visuals**: Displays large bold numbers (`24px`) with a small caps muted label (`11px`) explaining the data (e.g. Total Revenue, Booked Queue).

### 📈 CSS Bar Charts
* **Wrapper**: Flex row aligning bar columns to the bottom.
* **Bars**: Solid brand blue gradients (`#1a56db` to `#1240a0`) with height percentages representing clinical booking frequencies.
* **Labels**: Specialty icons (emojis) with text clipped to 6 characters.

### 📅 Data Tables
* **Header**: Off-white background (`var(--clr-bg)`), thin border under th (`1.5px`).
* **Rows**: Hover indicator changing row background slightly (`rgba(26,86,219,0.02)`) to indicate interactive rows.
* **Typography**: Medium weight table cells (`13.5px`) with monospace indicators for reference numbers.

### ⚙️ Modals & Overlays
* **Overlay**: Semi-transparent dark navy backdrop (`rgba(15,23,42,0.6)`) with `backdrop-filter: blur(4px)`.
* **Card**: Centered, max-width `500px` (or `550px` for prescriptions), rounded to `var(--radius-xl)` (`24px`). Animates in with a slide-up spring transition.

---

## 6. MOTION DESIGN TOKENS
* **Modal transition**: `all var(--t-base) (250ms ease)` animating opacity and translate values.
* **Chart bars height**: Dynamic transitions of `500ms ease` for bar load visual feel.
* **Tab fades**: Content panels fade in instantly to keep the user dashboard responsive.

---
*Design System Manual — MediCare HMS Portal*
*Built with HTML5 · CSS3 · Vanilla JavaScript (ES6+)*
