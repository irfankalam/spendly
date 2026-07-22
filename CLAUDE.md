# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Spendly is a Flask-based expense tracker, built incrementally as a step-by-step learning project (routes and comments reference "Step 1", "Step 3", etc.). Several routes are intentionally unimplemented placeholders — don't "complete" them unless asked; they mark future steps in the course.

## Commands

```bash
source venv/bin/activate        # virtualenv already exists at ./venv
pip install -r requirements.txt
python app.py                   # runs the dev server on http://localhost:5001 (debug=True)
```

There is no test suite yet, despite `pytest` and `pytest-flask` being listed in requirements.txt — they're there for when tests are introduced.

## Architecture

- **`app.py`** — single Flask application file with all routes. There is no blueprint/package structure; new routes get added directly here.
- **`database/db.py`** — currently a stub. It's meant to hold `get_db()` (SQLite connection with `row_factory` and foreign keys enabled), `init_db()` (`CREATE TABLE IF NOT EXISTS` statements), and `seed_db()` (sample data for dev). Not implemented yet.
- **`templates/`** — Jinja2 templates. `base.html` is the shared layout defining `{% block title %}`, `{% block head %}`, `{% block content %}`, and `{% block scripts %}`. All pages extend it and share one navbar/footer.
- **`static/css/style.css`** — shared/base styles used across all pages.
- **`static/css/landing.css`** — styles specific to the landing page only.
- **`static/js/main.js`** — intentionally near-empty. **Page-specific JavaScript does not go here** — it belongs inline inside that page's own `{% block scripts %}` in its template (see `templates/landing.html` for the pattern). Only add to `main.js` for behavior that's truly global/shared across pages.

## Conventions

- SQLite for storage (`*.db`/`*.sqlite*` are gitignored — no committed database file).
- No JS framework/bundler — plain `<script>` blocks per template.
