April Apakama
24/sci01/216
Online Laboratory Management System

*HOW THE PROJECT WORKS*
# Computer Laboratory Management System

A secure, server-rendered web application for running a university computer lab. Students and staff can book computers and report faults, while administrators approve bookings, manage equipment and users, and review an audit log.

Built for CSC 407 (Building Web Applications, Web Application Security, Testing, Deployment and Review) at Afe Babalola University.

**Live site** https://YOUR-APP.onrender.com

Note that the free Render plan sleeps when idle, so the first load can take a little while.

## What it does

### For lab users
- Register, log in and manage their own profile and password
- Browse computers with search and filters for keyword, status and location
- Request a booking for a time slot (15 minutes to 4 hours, up to 60 days ahead)
- Track, search and cancel their own bookings
- Report faulty machines with a severity level

### For administrators
- Add, edit and retire computers
- Approve or reject booking requests, with overlap checks to prevent double booking
- Review fault reports and update their status
- Change user roles and activate or deactivate accounts
- Search a full audit log of important actions

### For everyone
- A public Security page that explains each protection in the app
- A responsive layout that works on phones and desktops
- Clean error pages for 403, 404, 429 and 500


## Getting started

You need Node.js 22 or newer and Git.

```bash
git clone https://github.com/YOUR-USER/YOUR-REPO.git
cd YOUR-REPO
npm install
cp .env.example .env        # on Windows use  copy .env.example .env
npm run dev
```

Then open http://localhost:3000 in your browser.

### First start and demo accounts

On the first start the app creates the database and seeds it with one admin, three sample users and 20 computers.

If you leave the passwords empty in `.env`, random ones are generated in development and printed once in the terminal, so copy them right away. To start over, stop the app and delete the `data` folder.

| Role | Email |
|---|---|
| Admin | admin@lab.local (or whatever you set in ADMIN_EMAIL) |
| User | amara@lab.local |
| User | tunde@lab.local |
| User | chioma@lab.local |

## Configuration

All settings come from environment variables. Copy `.env.example` to `.env` for local use.

| Variable | Purpose |
|---|---|
| NODE_ENV | development or production |
| SESSION_SECRET | Signs session cookies and CSRF tokens (32 or more characters, required in production) |
| ADMIN_EMAIL | Email of the first admin |
| ADMIN_PASSWORD | Password of the first admin (required in production) |
| SEED_USER_PASSWORD | Optional shared password for the three sample users |
| DB_PATH | Location of the SQLite file, default `./data/lab.db` |
| PORT | Port to listen on, default 3000 |
| LOG_LEVEL | info by default, use debug to troubleshoot |

In production the app refuses to start without SESSION_SECRET and ADMIN_PASSWORD.

## Scripts

| Command | What it does |
|---|---|
| `npm run dev` | Start with automatic restart on changes |
| `npm start` | Start in production mode |
| `npm test` | Run the automated test suite |
| `npm run seed` | Seed an empty database by hand |
| `npm run backup` | Write a timestamped database backup to `./backups/` |



For a plain-language walkthrough, see [EXPLAINED.md](EXPLAINED.md).

## Testing

```bash
npm test
```

The suite has 302 automated tests across 15 suites, with about 96 percent line coverage of `src/`. It covers authentication, sessions, validation, access control, IDOR, SQL injection and XSS payloads, CSRF, rate limiting, lockout, error pages, log redaction and production configuration. Manual test tables are in [TESTING.md](TESTING.md).

## Deployment

The project deploys to Render straight from GitHub using the included `render.yaml` blueprint.

1. In Render choose New, then Blueprint, and select this repository.
2. Enter ADMIN_PASSWORD when prompted (and optionally SEED_USER_PASSWORD).
3. Click Apply and wait for the build.
4. Visit your onrender.com address and confirm `/health` returns `{"status":"ok"}`.

The full guide covers environment variables, HTTPS, custom domains and backups in [DEPLOYMENT.md](DEPLOYMENT.md).



More detail is in [REVIEW.md](REVIEW.md).

## Author
April Apakama
Built by April, final-year Computer Science student at Afe Babalola University, for CSC 407.

