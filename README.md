# KSU Wallet

A desktop student-wallet application built with Python (Tkinter for the UI,
SQLAlchemy + SQLite for storage). Students sign up, log in, and transfer
money between wallets; a separate admin panel manages KSU entities, pays
out student stipends, and cashes out entity balances.

## Features

- Student sign-up with validated Saudi phone numbers, KSU student email
  addresses, and 10-digit student IDs.
- Student login and wallet-to-wallet money transfers, with balance checks
  before every transfer.
- Admin panel to add KSU entities, view entity balances, pay a stipend to
  every student wallet at once, and cash out all KSU entity balances.
- Every transfer, stipend payout, and cash-out is recorded in a
  `transactions` table for a full audit trail.
- Passwords are never stored in plain text - they are hashed with
  PBKDF2-HMAC-SHA256 and a random per-user salt before being saved.

## Requirements

- Python 3.9+
- SQLAlchemy (`pip install -r requirements.txt`)

## Running it

```bash
pip install -r requirements.txt
python login_window.py
```

The first run creates `ksuwallet.db` (SQLite) in the project folder and
seeds one default admin account so the app is usable immediately:

- Admin ID: `1233211233`
- Password: `Admin123`

This is a demo account for local testing only - if you ever run this app
somewhere other people can reach, log in and change that password (or
remove the seeding block in `database_file.py`) before doing so.

## Project structure

| File | Purpose |
|---|---|
| `database_file.py` | SQLAlchemy models (`Wallet`, `Student`, `Admin`, `Entity`, `Transaction`) and DB setup. |
| `security.py` | Password hashing/verification helpers. |
| `DB_function.py` | All business logic: signup, login, transfers, stipends, cash-out. |
| `login_window.py` | Login screen. |
| `signup_window.py` | Student sign-up screen. |
| `StudentWalletWindow.py` | Student wallet view and transfer screen. |
| `admin_window.py` | Admin panel (entities, stipends, cash-out). |

## Notes / known limitations

- Storage is a local SQLite file, so data does not sync across machines -
  this is a single-machine demo, not a multi-user hosted service.
- There's no password-reset flow yet.
