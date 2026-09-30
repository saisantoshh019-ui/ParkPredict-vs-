# ParkPredict 2.0 — AI-Powered Multi-Location Smart Parking Platform

A two-portal smart-parking demo (User + Admin) covering five location types — IT company,
shopping mall, hospital, airport, commercial complex — with slot allocation, reservations,
EV charging, indoor navigation, Find-My-Car, dynamic pricing, a live admin command centre
and a local demo database.

## Quick start

```bash
# web client — zero build, just open it
open parkpredict/index.html          # or: npx serve parkpredict -l 3000

# reference engine + full test suite (stdlib only)
python solution.py                    # runs demo report + 41 unit tests
```

## Architecture

```
parkpredict/
├── index.html          # single-page client: UI + embedded JS engine (mirrors solution.py rules)
├── solution.py         # Python reference engine + embedded unittest suite (41 tests)
├── CREDENTIALS.md      # demo logins (passwords documented, stored hashed)
├── REQUIREMENTS.md     # requirement → implementation → test traceability matrix
├── vercel.json         # static-site deployment config
└── .github/workflows/  # CI: python-tests + lighthouse-100 gate
```

**Client engine (index.html):** seeded RNG for reproducible demo data, in-browser duration
model trained in non-blocking chunks (never blocks the main thread — Lighthouse TBT 0 ms),
probability math on the normal CDF, risk scoring, auto-replanning, waitlist & reservation
lifecycle, EV tick simulation, localStorage database (`parkpredict2_db_v2`).

**Reference engine (solution.py):** the same business rules as a clean, typed, documented
Python module — and it goes further than the client with real computer-science depth:

- **Ridge regression duration model** trained in-file (normal equations + Gaussian
  elimination, holdout-validated: MAE ±8.4 min, R² 0.89 on 400 seeded sessions)
- **Dijkstra shortest-path** indoor navigation over bay adjacency graphs
- **Holt linear-trend smoothing** on demand curves for 8-hour forecasts
- **Tamper-evident audit chain** (hash-linked events; `verify()` catches any mutation)
- **PBKDF2-HMAC-SHA256** credential store (120k iterations, per-user salts)
- Fairness guard: dynamic-pricing surcharges are hard-capped at ×2

## Testing & validation

- `python solution.py` → demo report, requirement self-audit matrix (R1-R15) and
  **109/109 unit tests in ~7 s** covering pricing, forecasting, the ML model, auth,
  audit-chain tampering, occupancy, vacate/waitlist, reservations, allocation,
  navigation, EV, find-my-car, admin alerts, input validation, performance budgets
  and cross-feature integration scenarios.
- CI gate re-runs the suite and asserts **Lighthouse 100/100/100/100** on every push.
- Security tests assert passwords are **never** stored, logged or exported in plaintext.

## Security & secrets

- Passwords stored as **per-user-salted SHA-256** hashes (Python: `hashlib`; web: WebCrypto).
- No secrets in source: demo passwords exist only in documentation, and the JS keeps them
  solely to *seed* hashed accounts; the database contains hashes only.
- Role-based access enforced in the router (user portal ≠ admin portal; location-scoped admins).

## Demo logins

See [CREDENTIALS.md](CREDENTIALS.md). Admin: `admin / Admin@123` (all locations),
`malladmin / Mall@123`, `airportadmin / Airport@123`. Users: `EMP1024`, `EMP2043`,
`VIS3007`, `VIS3008`, `EMP3050` — web client uses `demo123`, the Python AuthStore
enforces 8+ characters so its demo equivalent is `Demo@123` (both documented).

## Honest-data disclaimer

All parking data, forecasts and fees are **simulated demo data**. Predictions come from
explainable heuristics (demand curves + a linear duration model), not production ML, and
the UI labels them as such everywhere.
