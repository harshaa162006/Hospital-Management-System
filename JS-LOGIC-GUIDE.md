# JAVASCRIPT LOGIC GUIDE
## MediCare Hospital Management System (HMS)

This document breaks down the Javascript state managers, localStorage persistence handlers, role routers, queue tables, prescription writers, and admin CRUD logic.

---

## 1. PERSISTENCE LAYER (LOCALSTORAGE)

The system automatically initializes directories on page load if they are not already found in browser storage:

```javascript
// Example check for specialties directory
let SPECIALTIES = JSON.parse(localStorage.getItem('hms_specialties'));
if (!SPECIALTIES) {
  SPECIALTIES = [ /* Seed Array */ ];
  localStorage.setItem('hms_specialties', JSON.stringify(SPECIALTIES));
}
```

### Seeding Entries:
* `hms_specialties`: Seeds 6 clinical departments.
* `hms_doctors`: Seeds 12 verified specialist doctor profiles (2 per specialty).
* `hms_appointments`: Seeds 1 pending appointment record for test visibility.

---

## 2. PORTAL CONSOLE ROUTING (ROLE SWITCHING)

Navigating between dashboards is managed dynamically via `switchRole(role)`:

```javascript
function switchRole(role) {
  state.currentRole = role;

  // Toggle active class on role switcher header buttons
  document.querySelectorAll('.role-btn').forEach(btn => {
    btn.classList.toggle('active', btn.dataset.role === role);
  });

  // Toggle visible views
  document.querySelectorAll('.hms-view').forEach(view => {
    view.style.display = 'none';
  });

  if (role === 'patient') {
    document.getElementById('view-patient').style.display = 'block';
    showPatientSubView(state.currentPatientSubView);
  } else if (role === 'doctor') {
    document.getElementById('view-doctor').style.display = 'block';
    initDoctorDashboard();
  } else if (role === 'admin') {
    document.getElementById('view-admin').style.display = 'block';
    initAdminDashboard();
  }
}
```

---

## 3. PATIENT CONSOLE CONTROLLERS

### `showPatientSubView(view)`
Swaps patient interface between public landing page (wizard booking form) and "My Portal" dashboard.

### `renderPatientPortalData()`
* Extracts all bookings from `localStorage` under `APPOINTMENTS`.
* Sorts bookings chronologically (newest first).
* Populates:
  * **Appointments list**: Detail rows with status badges.
  * **Prescriptions list**: Lists appointments marked as `Completed` with a valid consultation object.
  * **Invoices list**: Details paid and pending items.

### `cancelAppointment(ref)`
Changes status to `Cancelled` in `localStorage` and alerts other active interfaces to update statistics.

---

## 4. CLINICAL DOCTOR CONTROLLERS

### `initDoctorDashboard()`
* Extracts doctor list from all specialties.
* Populates the active profile selector dropdown.
* Calls queue and availability renderers.

### `renderDoctorQueue()`
Filters the `APPOINTMENTS` collection to extract bookings belonging to `state.activeDoctor`. Completes check-ins or views prescription detail cards depending on consultation status.

### `submitConsultation(e)`
Gathers diagnosis string, medicine repeat rows, and clinical notes. Saves consultation details under the appointment object, marks state to `Completed`, updates browser database, and closes consultation card overlay.

```javascript
// Adding medicine row repeats dynamically
function addMedicineRow(name='', dosage='1-0-1', duration='5 days', notes='') {
  const container = document.getElementById('medicines-list-container');
  const rowId = 'med-row-' + Math.floor(Math.random() * 100000);
  
  const rowHtml = `
    <div class="med-row-inputs" id="${rowId}">
      <input type="text" placeholder="Medicine" class="form-input" required value="${name}" />
      <input type="text" placeholder="Dosage" class="form-input" required value="${dosage}" />
      <!-- Duration, Instructions columns and remove button -->
    </div>
  `;
  container.insertAdjacentHTML('beforeend', rowHtml);
}
```

---

## 5. ADMINISTRATIVE COMMAND CONTROLLERS

### `updateAdminStats()`
* Sums numerical consultation fee values of completed visits to calculate total revenue.
* Counts booking entries, completed checks, and cancellations.
* Renders a specialty bookings column chart by mapping appointment specialty counts to CSS element height percentages.

### `submitAddDoctor(e)`
Saves a new doctor profile under the selected specialty in `hms_doctors`. Generates initials and randomly applies color palettes for avatar credentials.

### `submitAddSpecialty(e)`
Saves a new department under `hms_specialties`. Initializes an empty array in the doctor listings database to prevent lookup exceptions.

### `filterAdminBookings()`
Queries the global log based on name/ref string, department filter select values, and booking status.

---
*JavaScript HMS Logic Guide*
