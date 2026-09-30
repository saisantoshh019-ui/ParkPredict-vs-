# ParkPredict 2.0 — Demo Login Credentials

All accounts live in the demo database (`localStorage`, key `parkpredict2_db_v1`) and are auto-seeded on first run. The **Admin → Database** tab shows every table; **Wipe & reseed** restores these defaults.

## 🛡️ Admin portal (Command Centre)

| Username | Password | Scope |
|---|---|---|
| `admin` | `Admin@123` | **All locations** (global) |
| `malladmin` | `Mall@123` | Shopping Mall only |
| `airportadmin` | `Airport@123` | Airport only |

**Sign-in steps:** open the app → on the **🔑 Login** page switch the portal toggle to **🛡️ Admin login** → enter username + password. The global `admin` opens the command centre at the location you were viewing (switch locations anytime from the header pill or Locations page). Location admins (`malladmin`, `airportadmin`) always land in their own location.

The admin sees: Overview (users, sessions, all-locations board), Parking Grid, ML Model, History, Waiting List, Reservations, Locations, Pricing, Analytics, System Alerts, Reports and the **Database** inspector.

## 🙋 User portal (Employees & visitors)

| Name | Login ID | Vehicle | Password | Location | Type |
|---|---|---|---|---|---|
| Rahul Kumar | `EMP1024` | TS09AB1234 | `demo123` | IT Company | Employee |
| Priya Sharma | `EMP2043` | AP28CD4455 | `demo123` | Hospital | Employee |
| Ananya Rao | `VIS3007` | TS09MB4321 | `demo123` | Shopping Mall | Visitor |
| Vikram Verma | `VIS3008` | KA05EV9090 | `demo123` | Airport | Visitor |
| Arjun Nair | `EMP3050` | TN09XY1122 | `demo123` | Commercial Complex | Employee |

**Sign-in steps:** open the **🔑 Login** page (nav button top-right), keep the **🙋 User login** tab, enter Name + Login ID + Vehicle number — no location picker; users land at their registered location automatically. One-click demo buttons (`EMP1024 · EMP2043 · VIS3007`) sit right under the form. Any new EMP/VIS ID self-registers on first login at the location you're currently viewing.

Users get their own dashboard (My Dashboard) with active parking, reservations, payments, quick actions — plus Find Parking, Reservations, EV Charging, Navigation/Find My Car and Mall mode. They cannot reach admin areas.

## 🗄️ Demo database

Collected tables (viewable in Admin → Database):

- `users` — all registered accounts
- `sessions` — every login/logout with role and location
- `reservations` — bookings with status lifecycle
- `parkingEvents` — entries, exits, vacates, cancellations, logins
- `payments` — demo fee transactions
- `settings` — platform metadata

Storage: browser `localStorage` (survives page reloads; you resume your last session within 12 hours). **Wipe & reseed** in the Database tab clears everything and restores the tables above. This is simulated demo persistence — not a production backend.
