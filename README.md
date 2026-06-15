# 🏥 MediCare Hospital — Fully Fledged Hospital Management System (HMS)
### Complete UI/UX Single-File HMS Portal Documentation

---

## 📋 TABLE OF CONTENTS

1. [Project Overview](#1-project-overview)
2. [Multi-Role Features List](#2-multi-role-features-list)
3. [Tech Stack](#3-tech-stack)
4. [File Structure](#4-file-structure)
5. [Database state & Data Models (localStorage)](#5-database-state--data-models-localstorage)
6. [Patient Portal Dashboard](#6-patient-portal-dashboard)
7. [Doctor Console Dashboard](#7-doctor-console-dashboard)
8. [Admin Console Dashboard](#8-admin-console-dashboard)
9. [Bug Fixes & Refinements](#9-bug-fixes--refinements)
10. [How to Run](#10-how-to-run)
11. [Accessibility & Responsiveness](#11-accessibility--responsiveness)
12. [Project Checklist](#12-project-checklist)

---

## 1. PROJECT OVERVIEW

The **MediCare Hospital Central Portal** is an advanced, single-file Hospital Management System (HMS) simulation. The application is built using a Single Page Application (SPA) structure, enabling real-time workspace transitions between Patients, Doctors, and Administrators.

State is globally shared and preserved dynamically through the browser's `localStorage` API, meaning that actions taken in one dashboard (such as booking an appointment as a patient) immediately impact other interfaces (appearing in the doctor's queue and updating the admin's revenue overview).

---

## 2. MULTI-ROLE FEATURES LIST

### 👤 Patient Portal
* **Guided Booking Wizard**: Specialty Selection → Doctor Selection → Date/Time Picker → Personal Details.
* **Portal Dashboard**: Toggleable view to manage active bookings.
* **My Appointments**: Live tracking of appointments with status badges (`Pending`, `Completed`, `Cancelled`). Patients can cancel pending appointments.
* **My Prescriptions**: Read-only access to prescription records (diagnosis, list of drugs with dosages, durations, and clinical notes) issued by doctors.
* **Billing & Receipts**: Automatically generated billing invoices showing consultation fees and transaction states (`Paid` at consultation, `Pending Counter Payment`, `Void`). Includes a browser print/save PDF shortcut.

### 👨‍⚕️ Doctor Dashboard
* **Profile Selection**: Dropdown to test different doctor schedules.
* **Live Patient Queue**: Shows patient listings, age, gender, reason for visit, and booking slot.
* **Consultation Console**: Interactive session form to write diagnoses, add rows of prescribed medicines (dosage, duration, instructions), write clinical notes, and complete check-ins.
* **Availability Toggle**: Controls portal visibility. Setting a profile to "On Leave" dynamically blocks patients from selecting that doctor in the booking calendar.

### 🔑 Admin Console
* **Analytics Cards**: Track hospital performance in real-time (Total Revenue generated from completed consultations, Total Appointments booked, Completed queue count, and Cancellations).
* **Booking Distribution Chart**: Custom CSS/SVG bar chart showing distribution of bookings across specialties.
* **Doctor Directory CRUD**: Add new doctor profiles (qualification, fee, experience, department) or remove active doctor listings.
* **Specialty Manager**: Add clinical departments with icons, description cards, and estimated wait times.
* **Global Appointment Logs**: Master database table with search capabilities and filtering options (by department and booking status).

---

## 3. TECH STACK

```
Language    : HTML5, CSS3, JavaScript (ES6+)
Persistence : Browser localStorage (JSON serialization)
Fonts       : Google Fonts (Instrument Serif + DM Sans)
Icons       : Inline SVG + Emojis (no heavy dependencies)
Dependencies: ZERO external javascript libraries
Build Tools : NONE — open directly in any modern browser
```

---

## 4. FILE STRUCTURE

```
hospital-appointment-system/
│
├── hospital-appointment-system.html   ← ENTIRE APPLICATION (HTML + CSS + JS)
├── README.md                          ← This document
├── CSS-REFERENCE.md                   ← Dashboard styles & tokens documentation
├── JS-LOGIC-GUIDE.md                  ← Javascript State, CRUD, and Modal controllers
└── DESIGN-SYSTEM.md                   ← Layout grids, colors, and accessibility tokens
```

---

## 5. DATABASE STATE & DATA MODELS (LOCALSTORAGE)

Data is persisted inside local storage keys:
1. `hms_specialties`: Collection of clinical departments.
2. `hms_doctors`: Map of doctor objects, keyed by specialty code.
3. `hms_appointments`: Global collection of booked patient records.

### Appointment Record Schema
```javascript
{
  ref: "MC-381045",              // 6-digit random reference
  patientName: "Arjun Sharma",   // Full patient name
  dob: "1990-05-15",             // Date of Birth
  gender: "Male",                // Patient gender
  phone: "9876543210",           // Indian mobile number
  email: "arjun@example.com",    // Email address
  specialtyId: "cardiology",     // Specialty ID key
  specialtyName: "Cardiology",   // Specialty display name
  doctorName: "Dr. Priya Menon", // Chosen Doctor
  doctorIdx: 0,                  // Doctor index in localStorage array
  date: "June 25, 2026",         // Visit date
  time: "10:00 AM",              // Slot time
  fee: "₹800",                   // Outpatient consultation fee
  reason: "Routine check-up",    // Selected symptom pill
  notes: "Occasional tightness",  // Text notes
  status: "Pending",             // Status: 'Pending' | 'Completed' | 'Cancelled'
  timestamp: 1779948000000,      // Booking epoch timestamp
  consultation: {                // Added by Doctor upon completion
    diagnosis: "Pre-hypertension",
    medicines: [
      { name: "Amlodipine", dosage: "1-0-0", duration: "10 days", notes: "After food" }
    ],
    clinicalNotes: "Monitor BP weekly.",
    consultedAt: "15/06/2026"
  }
}
```

---

## 6. PATIENT PORTAL DASHBOARD
Patients can navigate between the public **Book Appointment** wizard and **My Portal**. 
When an appointment is completed by a doctor, the status indicator in "My Portal" changes to `Completed`. The patient can immediately click **View Prescription** to open the doctor's prescription slip or **Print Invoice** to download their receipt.

---

## 7. DOCTOR CONSOLE DASHBOARD
Doctors log in and select their profile to view their custom queue. Clicking **Consult** opens the Consultation workspace modal. Doctors write the diagnosis and add medicine rows using an interactive row repeater. Clicking **Submit Consultation** updates the local storage, shifts the patient status to `Completed`, and notifies the patient portal.

---

## 8. ADMIN CONSOLE DASHBOARD
Provides central oversight of hospital statistics. Admins can view analytics cards, add doctor profiles to active departments, add new specialties, and review all booking transactions.

---

## 9. BUG FIXES & REFINEMENTS

The system addresses several critical UI/UX and logic bugs present in earlier prototypes:
* **Past Month Navigation Blocked**: In the Date selection step, navigation to months prior to the current system date is disabled in the calendar.
* **Date of Birth Limit**: The Date of Birth input field dynamically restricts users from selecting future birthdates.
* **Indian Mobile Number Validation**: The form validates mobile inputs using a standard Indian phone regex (`/^[6-9]\d{9}$/`).
* **Leave/Availability Block**: If a doctor's availability is set to "On Leave", the doctor card in Step 2 is greyed out and disabled.

---

## 10. HOW TO RUN

1. Open `hospital-appointment-system.html` directly by double-clicking it in your file explorer.
2. The role switcher at the very top of the window allows you to switch between **Patient**, **Doctor**, and **Admin** workspaces.

---

## 11. ACCESSIBILITY & RESPONSIVENESS

* **ARIA Controls**: Dashboard tabs, custom modal forms, and role switchers utilize appropriate role attributes (`role="gridcell"`, `aria-live="polite"`).
* **Keyboard Navigation**: Modals support focus containment, and interactive cards allow Enter/Spacebar controls.
* **Fluid Layouts**: Grids automatically wrap from 2-column sidebar structures to single-column phone interfaces below `768px`.

---

## 12. PROJECT CHECKLIST

* [x] Shared state database via `localStorage`
* [x] Interactive Role switching bar
* [x] Patient Booking Wizard + "My Portal" dashboard
* [x] Doctor Queue, Status Toggles, and Prescription modal writer
* [x] Admin overview cards, dynamic simulated charts, and directories CRUD
* [x] Indian Phone number & future DOB calendar validation fixes
* [x] Fully responsive layout with automatic dark mode support

---
*MediCare HMS Portal — UI/UX & Clinical Management System*
*Built with HTML5 · CSS3 · Vanilla JavaScript (ES6+)*
*© 2026 — Nellore, Andhra Pradesh*
