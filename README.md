# ⚜️ GrandSouk — The Auction Chamber

> Teyzix Core Internship · Task FS-2 · Full-Stack Web Development

**GrandSouk** is a luxury auction-house themed Vendor Management & Quotation System. Instead of generic dashboards and vendor tables, it reimagines the entire experience as a grand trading chamber where companies are *Houses*, quotations are *Proposal Scrolls*, and the comparison view is the *Grand Duel*.

---

## Concept

| Generic Term     | GrandSouk Term     |
|------------------|--------------------|
| Vendor           | House              |
| Company Name     | Estate Title       |
| Email            | Seal               |
| Contact Number   | Envoy              |
| Address          | Quarters           |
| Quotation        | Proposal Scroll    |
| Description      | Decree             |
| Amount           | Bid (Ducats)       |
| Status           | Verdict            |
| Approved         | Sanctioned         |
| Rejected         | Declined           |
| Notes            | Chamber Notes      |
| Activity Log     | Grand Ledger       |
| Dashboard        | The Chamber        |
| Compare View     | Grand Duel         |

---

## Tech Stack

| Layer     | Technology                      |
|-----------|---------------------------------|
| Frontend  | React 18, React Router v6       |
| Backend   | Node.js, Express.js             |
| Database  | MongoDB + Mongoose              |
| Auth      | JWT + bcryptjs                  |
| Fonts     | Cinzel (headings), EB Garamond  |
| FX        | Canvas gold dust particles      |

---

## Unique Design Features

- **Cinzel serif** typeface for all headings — classical Roman engraving feel
- **EB Garamond** for body text — antique manuscript aesthetic
- **Canvas gold dust** — floating particles rendered in `<canvas>` on page load
- **Dark gold colour palette** — `#07060a` bg, `#d4af37` gold, `#9b2335` crimson
- **Tier system** for Houses — Bronze, Silver, Gold, Platinum with distinct badge colours
- **Grand Duel** comparison view — ranked by bid with a 👑 Victor crown on the lowest
- **Ducat currency** — bids displayed as "Ducats" for immersive feel
- All actions use thematic language — *Induct, Expel, Sanctioned, Burned*

---

## Project Structure

```
grandsouk/
├── backend/
│   ├── models/         User, House, Proposal, Ledger
│   ├── routes/         auth, houses, proposals, chamber
│   ├── middleware/     auth.js (JWT)
│   ├── server.js
│   └── .env.example
└── frontend/
    ├── public/         index.html (canvas dust particles)
    └── src/
        ├── components/ Sidebar.jsx
        ├── context/    AuthContext.jsx
        ├── pages/      AuthPage, Chamber, Houses, Proposals, Duel
        ├── utils/      api.js
        └── App.jsx
```

---

## Database Schema

### House (Vendor)
| Field       | Type   | Notes              |
|-------------|--------|--------------------|
| houseName   | String | Vendor name        |
| estateTitle | String | Company name       |
| seal        | String | Email (unique)     |
| envoy       | String | Contact number     |
| quarters    | String | Business address   |
| standing    | String | active / suspended |
| tier        | String | bronze/silver/gold/platinum |
| speciality  | String | Optional           |

### Proposal (Quotation)
| Field       | Type     | Notes                              |
|-------------|----------|------------------------------------|
| scrollTitle | String   | Quotation title                    |
| decree      | String   | Description                        |
| house       | ObjectId | Ref → House                        |
| bidAmount   | Number   | Quotation amount (Ducats)          |
| sealedOn    | Date     | Submission date                    |
| verdict     | String   | pending/submitted/sanctioned/declined |
| chamber     | String   | Private notes                      |

---

## Setup & Run

### Prerequisites
- Node.js v18+  ·  MongoDB (local or Atlas)

### Backend
```bash
cd grandsouk/backend
cp .env.example .env       # set MONGO_URI and JWT_SECRET
npm install
npm run dev                # http://localhost:5000
```

### Frontend
```bash
cd grandsouk/frontend
npm install
npm start                  # http://localhost:3000
```

---

## API Reference

### Auth
| POST | `/api/auth/register` | Register |
| POST | `/api/auth/login`    | Login    |

### Houses
| GET    | `/api/houses`        | List (search, standing, tier filters) |
| POST   | `/api/houses`        | Induct new house |
| PUT    | `/api/houses/:id`    | Amend records    |
| DELETE | `/api/houses/:id`    | Expel house      |

### Proposals
| GET    | `/api/proposals`      | List (search, verdict filters) |
| GET    | `/api/proposals/duel` | Grand Duel — submitted/sanctioned sorted by bid |
| POST   | `/api/proposals`      | Issue scroll   |
| PUT    | `/api/proposals/:id`  | Amend scroll   |
| DELETE | `/api/proposals/:id`  | Burn scroll    |

### Chamber (Dashboard)
| GET | `/api/chamber` | Stats + Grand Ledger |

---

*Built for Teyzix Core Internship — June Batch 2026*
