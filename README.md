# 🏥 MediFlow — Clinic Management System

A web-based clinic management system built with **HTML, CSS, Vanilla JS** and **Firebase** for the Unified Mentor internship project.

---

## 🚀 Live Demo

Open `index.html` in any modern browser — no build step required.

---

## 📋 Features

| Feature | Role |
|---|---|
| Role-based login (Doctor / Receptionist) | Both |
| Register patients + auto token generation | Receptionist |
| Patient queue view | Doctor |
| Write & save prescriptions | Doctor |
| Generate itemized bills | Receptionist |
| Patient history search | Both |
| Real-time Firestore database | Both |
| Logging of all actions | System |

---

## 🛠 Tech Stack

- **Frontend**: HTML5, CSS3, Vanilla JavaScript (ES Modules)
- **Backend / Database**: Firebase Firestore (NoSQL)
- **Auth**: Firebase Authentication (Email/Password)
- **Logging**: Console + SessionStorage logger

---

## 🏗 System Architecture

```
Browser (HTML/CSS/JS)
        │
        ▼
Firebase Auth ──► Role stored in Firestore users collection
        │
Firebase Firestore
    ├── users        (uid, email, role)
    ├── patients     (name, age, gender, token, status, ...)
    ├── prescriptions (patientId, diagnosis, medications, ...)
    └── bills         (patientId, consult, lab, meds, total, ...)
```

---

## 🔄 Workflow

1. **Receptionist** registers → creates account with `receptionist` role
2. **Doctor** registers → creates account with `doctor` role
3. Receptionist logs in → registers patients → system auto-assigns token (e.g. `TK-20250218-001`)
4. Doctor logs in → sees today's queue → writes prescriptions
5. Receptionist sees updated status → generates bills
6. Both users can search full patient history anytime

---

## 📁 File Structure

```
clinic-management/
└── index.html       # Complete single-file app (all HTML + CSS + JS)
```

---

## ▶ Running Locally

1. Clone the repo
2. Open `index.html` in a browser (Chrome/Firefox/Edge)
3. Register as Doctor or Receptionist
4. Start managing patients!

> No local server required — Firebase SDK loads via CDN.

---

## 🧪 Test Cases

| Test | Expected Result |
|---|---|
| Register with valid email+pass | Account created, redirected to dashboard |
| Register with existing email | Error message shown |
| Register patient without name | Validation error |
| Register patient | Token auto-generated (TK-YYYYMMDD-NNN) |
| Write prescription without diagnosis | Validation error |
| Generate bill | Total auto-calculated, saved to Firestore |
| Search by name/token | Matching patients shown with full history |

---

## 📊 Logging

All user actions are logged with timestamps to the browser console and `sessionStorage`:

```
[2025-02-18T10:30:00Z] [INFO] User signed in: doctor@clinic.com
[2025-02-18T10:31:00Z] [INFO] Patient registered: John Doe Token: TK-20250218-001
[2025-02-18T10:35:00Z] [INFO] Prescription saved for: John Doe
```

---

## ⚙ Firebase Firestore Rules (Recommended)

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

---

## 👤 Author

Built for Unified Mentor Internship — Clinic Management System project.
