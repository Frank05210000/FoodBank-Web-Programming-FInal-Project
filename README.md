# Food Bank Booking System

A Flask + PostgreSQL platform that lets the public reserve near-expiry food, enables shops to manage listings and orders, and gives administrators a console to monitor site-wide activity.

## Motivation
Taiwan discards large amounts of food every day—from supermarkets to convenience stores—because items are nearing or just past their best-before dates. Studies estimate 3.6–3.8 million tons of waste annually; stacked in buckets, that would exceed the height of thirteen thousand five hundred Taipei 101 buildings. Much of this perfectly edible food ends up as trash.

Meanwhile, about 260,000 low- and lower-income households still struggle to secure meals and need stable, dignified food support. If we can redirect food that remains within a safe consumption window through a robust management system—from convenience stores, hypermarkets, or households—to those in need, we reduce waste while supporting vulnerable groups. This project aims to build a user-friendly “Food Bank” website to connect donors and recipients so resources are distributed more efficiently.

## Features
- Public users: register/login, view map and nearby locations, browse shop pages, add to cart, checkout reservations, view order history, manage account.
- Shop owners: apply for an account; list, edit, or remove items; view orders and mark them complete or cancelled.
- Administrators: dashboard stats, latest orders, delete shops and users, intervene to cancel orders.
- Multi-language: English/Chinese UI with a navbar toggle (default English).

## Stack
- **Backend**: Flask, Flask-Login, Flask-Migrate, SQLAlchemy
- **Database**: PostgreSQL (configurable via `DATABASE_URL`)
- **Frontend**: Bootstrap 5, Leaflet.js, vanilla JS/CSS

## Project Layout
```
├── app.py                # Flask entrypoint and routes
├── config.py             # Config (Postgres/Secret)
├── extensions.py         # db/migrate initialization
├── models.py             # SQLAlchemy models
├── seed.py               # Fake data generator
├── requirements.txt      # Dependencies
├── migrations/           # Alembic migration records
├── templates/            # Jinja2 templates (pages)
├── static/
│   ├── css/style.css     # Custom styles
│   └── js/script.js      # Leaflet/interaction scripts
├── tests/                # pytest suite
├── docs/                 # Docs (SETUP, TESTING, specs, assignment)
├── ref/                  # Reference samples
└── README.md             # Project overview (this file)
```

## Quick Start
See `docs/SETUP.md` for environment setup, database initialization, and loading seed data. Demo accounts are listed in `docs/ACCOUNTS.md`.

After starting the server at `http://localhost:5001/` you can try:
- Public user: `user@example.com` / `password`
- Shop owner: `shop1@example.com` / `password`
- Administrator: `admin@example.com` / `admin123`

## Testing
The project ships with two levels of automated tests via `pytest`:

- **Unit Test**: verifies `Shop.available_quantity` only counts active items with stock.
- **Integration Test**: simulates the full reservation flow (login → add to cart → checkout) and checks an `Order` is created and inventory is decremented.

Run tests with:
```bash
source venv/bin/activate
pytest
```

## Development Notes
- After modifying models, run `flask --app app.py db migrate` to generate migrations, then `db upgrade` to apply them.
- To add more shops/items, edit `seed.py` and rerun it.
- Automated tests are minimal; feel free to expand pytest coverage or further improve UI/flows/internationalization.
