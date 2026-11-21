# CareLedger

A full-stack health expense and insurance manager. Track medical bills, insurance claims, prescriptions and appointments, set a monthly health budget, and see where your money goes.

**Stack:** Flask (Python) · SQLite · JWT auth · vanilla JS single-page frontend

## Features
- Register / login with hashed passwords and JWT sessions (7-day expiry)
- Role-based access: normal users and an admin panel with platform stats
- Full CRUD for bills, insurance claims, prescriptions and appointments (per-user data isolation)
- Dashboard: monthly spend, unpaid bills, insurance recovered, 6-month trend, spend by category, upcoming visits, refills due this week
- Monthly budget with progress meter
- Search on every list, CSV export for bills
- Input validation, JSON error handling, unit tests

## Run it
```bash
python -m venv venv && source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt
python app.py
```
Open http://localhost:5000. Demo data is created on first run:

| Account | Email | Password |
|---|---|---|
| Patient | demo@careledger.dev | demo1234 |
| Admin | admin@careledger.dev | admin1234 |

Set the variables from `.env.example` in your environment, and use a real `SECRET_KEY` before deploying.

## Tests
```bash
python -m unittest tests.test_api
```

## API
All routes except auth need `Authorization: Bearer <token>`.

| Method | Route | Purpose |
|---|---|---|
| POST | `/api/auth/register`, `/api/auth/login` | Create account / sign in |
| GET | `/api/auth/me` | Current user |
| GET POST | `/api/{bills,claims,prescriptions,appointments}` | List / create |
| PUT DELETE | `/api/{resource}/<id>` | Update / delete |
| GET | `/api/bills/export.csv` | Download bills |
| GET PUT | `/api/budget` | Monthly limit |
| GET | `/api/dashboard` | Summary numbers and charts data |
| GET | `/api/admin/stats` | Admin only |

## Structure
```
app.py          API, schema, auth, seed data
static/         index.html, style.css, app.js (SPA)
tests/          API tests
```
