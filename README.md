# NEXUS — Starter application

A Persian RTL, dark GitHub-inspired starter web app with a Python standard-library HTTP server, SQLite persistence, scrypt password hashing, atomic first-account founder assignment, a timed multiple-choice game, server-side answer scoring, and a persistent leaderboard.

## Run locally

Requirements: Python 3.10+ (no pip packages required).

```bash
python server.py
```

Open http://127.0.0.1:8000. The SQLite database is created automatically as `nexus.sqlite3`.

## Included in this milestone

- Responsive Persian RTL interface and dark/light theme toggle.
- The supplied first portrait is used for login/registration; the second portrait is used on the homepage.
- Account creation and login with username/password; passwords are stored as salted scrypt hashes, never plaintext.
- Atomic first successful registration receives `FOUNDER` via SQLite `BEGIN IMMEDIATE` and a unique singleton ownership record. Later accounts receive `USER`.
- HttpOnly, SameSite session cookie; server-side role check for founder panel.
- Timed multiple-choice quiz, server-side answer verification, persistent scores/results, leaderboard.
- Profile dashboard, starter achievements UI, founder account list.

## Important limitations before public deployment

This is a runnable local starter, **not yet production-hardened**. The session store is in memory and sessions end when the server restarts. Add a durable session store, HTTPS and `Secure` cookies, CSRF protection/origin validation, login/register rate limiting, password reset, account suspension, full audit log views, migration/backup tooling, and automated tests before public deployment. The game server currently validates the submitted answer array and ignores client-provided score, but a robust competitive version must persist server-issued game sessions, question delivery state, deadlines, and idempotency keys to prevent replay and enforce timer integrity. The quiz uses a small fixed sample set. Additional advertised modes are explicitly marked as not implemented. The founder panel currently has read-only user listing; no destructive admin actions are included.

For local testing, use `127.0.0.1`. To expose this app publicly, place it behind a properly configured HTTPS reverse proxy and harden the application first.
