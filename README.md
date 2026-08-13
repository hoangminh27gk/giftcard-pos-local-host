# Giftcard POS

A simple, self-hosted point-of-sale web app for managing store gift cards —
charge, refill, track balances, and print receipts.

## Features

- **Charge / Refill** — look up a card by code or MSR ID, charge a purchase,
  or add balance back
- **All Cards** — search, edit, remove, and print the current balance of any card
- **History** — every transaction (charge, refill, add, remove), grouped by
  day and collapsible, with search/filter and reprint
- **Add Card / Import** — add cards manually or bulk-import from an Excel
  file (a downloadable template is built in)
- **Receipt printing** — print via the browser's print dialog, or connect a
  USB thermal receipt printer directly (ESC/POS, via WebUSB) for instant,
  no-dialog printing
- **Settings** — business name/address/phone (shown on receipts), login
  credentials, and printing preferences, all editable from the app

## Running locally

```
python -m venv .venv
.venv\Scripts\activate      # Windows
# source .venv/bin/activate # macOS/Linux

pip install Flask SQLAlchemy openpyxl
python app.py
```

Open http://localhost:5000 — default login is `admin` / `password123!`
(change both business info and login credentials from the in-app **Settings**
tab, or via the `APP_USERNAME` / `APP_PASSWORD` environment variables).

The app uses SQLite locally (`giftcards.db`, created automatically, not
committed to git) and PostgreSQL in production via `DATABASE_URL`.

> `psycopg2-binary` and `gunicorn` (in `requirements.txt`) are only needed for
> production/Postgres deploys — skip them for local SQLite development.

## Deploying

See [DEPLOY_GUIDE.md](DEPLOY_GUIDE.md) for step-by-step instructions to put
this on GitHub and deploy it to Render with a managed PostgreSQL database.

## Tech stack

Flask + SQLAlchemy (SQLite locally / PostgreSQL in production), vanilla
JS/HTML/CSS frontend (no build step), openpyxl for Excel import/export.
