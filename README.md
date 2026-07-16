# Mis Gastos App

> This project was built during university studies. Code comments and variable names are in Spanish, while this documentation is in English for accessibility.

A personal finance management mobile application built with **Flutter** (frontend) and **Flask** (backend). It allows users to track expenses and incomes, visualize their balance, and manage recurring income entries — with Firebase powering the mobile auth & data layer, and a MySQL-backed Flask API providing an alternative backend.

---

## Tech Stack

### Mobile App (Flutter)

- **Framework:** Flutter (Dart)
- **State Management:** GetX
- **Architecture:** Clean Architecture (domain, data, presentation layers)
- **Authentication:** Firebase Auth (email/password)
- **Database:** Cloud Firestore
- **Charts:** fl_chart
- **Calendar:** table_calendar

### Backend (Flask)

- **Framework:** Flask 3.0.2
- **ORM:** SQLAlchemy 2.0.29 + Flask-SQLAlchemy
- **Serialization:** Marshmallow
- **Database:** MySQL 8.0
- **Deployment:** Docker Compose

---

## Features

- User registration and login (Firebase Auth)
- Add, view, and delete expenses
- Add, view, and delete incomes with recurrence (unique, weekly, biweekly, monthly)
- Calendar view with expenses grouped by date
- Dashboard with income total, balance, and bar chart visualization
- Combined expense/income history with swipe-to-delete
- Dark mode support
- Flask REST API backend with MySQL

---

## Project Structure

```
misgastosapp/
├── lib/
│   ├── main.dart                    # App entry point
│   ├── firebase_options.dart        # Firebase configuration
│   ├── app/
│   │   ├── domain/                  # Entities, repositories, use cases
│   │   ├── data/                    # Models, datasources, repository implementations
│   │   └── presentation/            # Controllers, pages, widgets
│   └── core/
│       ├── bindings/                # GetX dependency injection
│       ├── routes/                  # Route definitions
│       ├── services/                # Service stubs
│       └── themes/                  # Light and dark themes
├── backend/
│   ├── app/                         # Flask application
│   ├── docker-compose.yml           # Docker setup
│   ├── Dockerfile
│   ├── requirements.txt
│   └── .env
├── android/
├── ios/
├── web/
├── test/
└── pubspec.yaml
```

---

## Screens

| Screen | Route | Description |
|--------|-------|-------------|
| Session Check | `/check` | Redirects based on auth state (login or home) |
| Welcome | `/` | Splash with app logo and "Get Started" button |
| Login | `/login` | Email/password login form |
| Register | `/register` | Registration with name, age, country |
| Home | `/home` | Dashboard with balance, chart, and bottom navigation |
| Add Expense | (tab) | Quick expense entry form |
| Calendar | (tab) | Monthly calendar with expenses per day |
| Expense History | (navigated) | Combined chronological list of all movements |
| Income List | (navigated) | Manage incomes with recurrence settings |

---

## Firebase Structure

```
usuarios/{uid}                    # User profile
├── nombre: string
├── correo: string
├── edad: int
├── pais: string
├── gastos/{docId}               # Expenses subcollection
│   ├── monto: double
│   ├── descripcion: string
│   └── fecha: Timestamp
└── ingresos/{docId}             # Incomes subcollection
    ├── monto: double
    ├── descripcion: string
    ├── fechaInicio: Timestamp
    └── frecuencia: string       # "unico", "semanal", "quincenal", "mensual"
```

---

## Running the Mobile App

```bash
# Install dependencies
flutter pub get

# Run on Android
flutter run
```

> **Note:** Firebase is currently configured only for Android.

---

## Running the Backend

```bash
cd backend

# Using Docker (recommended)
docker-compose up --build

# Or manually
pip install -r requirements.txt
python app/main.py
```

The API will be available at `http://localhost:5000`.

### Backend API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/auth/register` | Register a new user |
| `POST` | `/api/auth/login` | Login |
| `POST` | `/api/expenses/` | Create an expense |
| `GET` | `/api/expenses/` | Get expenses by user |

---

## Dependencies

### Flutter (key packages)

- `get` - State management and routing
- `firebase_core`, `firebase_auth`, `cloud_firestore` - Firebase services
- `table_calendar` - Calendar widget
- `fl_chart` - Charts

### Python (key packages)

- `Flask` 3.0.2 - Web framework
- `SQLAlchemy` 2.0.29 - ORM
- `PyMySQL` 1.1.0 - MySQL driver
- `marshmallow` 3.21.1 - Serialization
