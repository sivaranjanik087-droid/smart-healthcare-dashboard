# Healthcare Dashboard

> Real-time healthcare operations command centre with AI-assisted decision support — a single unified view over ICU, triage, pharmacy, staffing, emergency ops and capacity, with a role-aware AI copilot.

**Live demo (always open, no login required to view):** [https://smart-healthcare-dashboard-eight.vercel.app](https://smart-healthcare-dashboard-eight.vercel.app)

**Mirror deployment:** [https://dao-voting-portal.vercel.app](https://dao-voting-portal.vercel.app)

![Deployment](https://img.shields.io/badge/deployment-Vercel-000000?logo=vercel&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Web-4FC08D)
![React](https://img.shields.io/badge/React-18-blue?logo=react&logoColor=white)
![Vite](https://img.shields.io/badge/Build-Vite-646CFF?logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Styling-Tailwind_CSS-06B6D4?logo=tailwindcss&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue)

---

## Project Overview

**Healthcare Dashboard** (internally *AURA AI Healthcare Command Center*) is a self-contained web command centre for hospital operations. It fuses live operational telemetry — patient flow, bed capacity, ICU vitals, pharmacy inventories, blood stock, staffing and emergency triage — into one responsive dashboard. Every module respects the signed-in user's role, and an AI copilot ("Operations Assistant") explains state and suggests actions from the active data.

The project is delivered as a **pre-built, framework-agnostic static bundle**: `index.html` + `assets/`. It runs with zero build steps on any static host, and deploys to the always-on URL above.

> ⚠️ **Research prototype.** All data is synthetic or simulated; credentials are validated client-side only. Not certified for clinical decision-making.

---

## Demo Accounts (role-based access)

Sign in with any of these demo accounts — each role only sees the modules it is authorised for.

| Role | Username | Password | Access scopes |
| --- | --- | --- | --- |
| **Admin** | `admin` | `admin123` | Full command-centre access — all modules |
| **Doctor** | `doctor` | `doctor123` | Clinical modules (ICU, triage, patient flow) |
| **Nurse** | `nurse` | `nurse123` | Bedside ops, capacity, vitals |
| **Lab Tech** | `labtech` | `lab123` | Laboratory-related modules |
| **Pharmacist** | `pharmacist` | `pharm123` | Pharmacy & blood stock |
| **Reception** | `reception` | `recp123` | Front-desk, patient flow |

Passwords never leave the browser — the dashboard validates against a built-in demo account store.

---

## Key Features

| Area | What it does |
| --- | --- |
| **Command Center** | Executive operational overview: health score, active alerts, capacity and pressure indicators |
| **Emergency Ops** | Live incident pressure, triage intake by severity, "free bed" response actions |
| **Digital Twin & Capacity** | What-if editing of hospital metrics (beds, staff, admissions) with instant knock-on effects |
| **Manual Data Control** | Real-time hospital telemetry entry — values you enter are respected exactly* |
| **ICU Command** | Per-ICU patient snapshots with current vitals from a centralised state store |
| **Pharmacy & Blood** | Drug inventory, low-stock/expiry alerts, blood units on hand |
| **Emergency Triage** | Severity-prioritised triage queue and workload tracking |
| **Staff & Availability** | Shift rosters, workload index, staffing gaps |
| **Reports** | Human-readable operational reports, printable |
| **AI Copilot** | Natural-language operations assistant over the active dashboard state |

\* See Data Modes below — manual inputs are honoured in manual mode; automatic simulation drift runs only in simulated mode.

### Data Modes
- **Manual** — edits and inputs you make are persisted in-browser and respected exactly.
- **Simulated** — automatic operational drift generates a realistic live synthetic feed.

### Current Shift Presets
- 🌅 Morning · 🌇 Evening · 🌙 Night shift profiles switch the operational context instantly.

---

## Tech Stack

- **Framework:** React 18 (compiled, ES-module bundle)
- **Language:** TypeScript
- **Build tool:** Vite
- **Styling:** Tailwind CSS (compiled)
- **State:** Zustand-style centralised, persisted store
- **Charts & icons:** Recharts-style data visualisation + Lucide-style icon components
- **Icons:** SVG icon set (no emoji-based UI text)
- **Typography:** Self-hosted **Inter** (weights 100–900), enforced globally by `assets/fonts/override.css`
- **Hosting:** Vercel (static, framework-agnostic, always-on)

---

## Project Structure

```
.
├── index.html              # Application shell (loads bundle + fonts)
├── assets/
│   ├── index-C7bjNmL1.js   # Compiled application bundle (all screens)
│   ├── index-DrCZDLUa.css  # Compiled Tailwind/component styles
│   └── fonts/
│       ├── fonts.css       # @font-face declarations for self-hosted Inter
│       ├── override.css    # Global font lock: one consistent Inter face app-wide
│       └── inter/          # Inter variable woff2 files (latin + latin-ext)
├── vercel.json             # Vercel static-site configuration + cache headers
├── index.html
├── .gitignore
├── LICENSE                 # MIT
└── README.md
```

---

## Code Overview

The application is distributed as a compiled static build — on purpose. The single `assets/index-C7bjNmL1.js` module implements the entire UI: role-based authentication, the route-per-module shell, the persisted state store, the simulation tick engine, the AI copilot prompt/response flow, and every screen (Command Center → Reports).

Global typography is controlled centrally rather than per-component:

```css
/* assets/fonts/override.css */
* { font-family: 'Inter', Arial, system-ui, sans-serif !important; }
```

This guarantees every surface — login, dashboard, sidebar, navbar, cards, tables, buttons, forms, modals, charts and notifications — renders the identical font. A data-integrity pass also repaired all double-encoded Unicode in the bundle, so punctuation, dashes and role icons render correctly.

---

## Getting Started

### Option A — Run locally (static)

```bash
# Node.js
npx serve .

# or Python
python -m http.server 8080
```

Open [http://localhost:8080](http://localhost:8080) and sign in with any demo account above.

### Option B — Deploy to Vercel

1. Import this repository into Vercel.
2. `vercel.json` declares a framework-agnostic static deployment (`frameworks: null`), so no build command is required.
3. The site is served immediately and stays reachable at the deployment URL.

### Option C — Deploy from CLI (as used for this project)

```bash
vercel deploy --prod --yes
```

---

## Live Deployment

- **Production:** https://smart-healthcare-dashboard-eight.vercel.app
- **Mirror:** https://dao-voting-portal.vercel.app
- **Config:** `vercel.json`

Cache headers are configured so the HTML and font stylesheets are always served fresh (`no-store`), meaning updates appear immediately without stale-cache issues.

---

## Roadmap

- [x] Module shell — Dashboard / Command Center / Emergency Ops / Capacity / ICU / Pharmacy & Blood / Triage / Staff / Reports
- [x] Role-based access with demo accounts
- [x] Manual + simulated data modes
- [x] AI copilot operations assistant
- [x] Self-hosted fonts, consistent app-wide typography
- [x] Static bundle + always-on Vercel deployment
- [ ] Live data connectors (EMR / HL7 FHIR)
- [ ] Real authentication provider
- [ ] Real-time telemetry via WebSockets

---

## License

Distributed under the [MIT License](LICENSE).

## Disclaimer

Demonstration / research prototype. All data shown is synthetic or simulated and the dashboard is **not** certified for clinical decision-making. Do not use for real patient care.