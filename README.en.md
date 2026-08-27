<div align="center">

# Davam

**Integrated Maintenance Management System for Drilling Rigs**

[فارسی](README.md) · English · [Landing page](https://m0000hamad.github.io/davam-showcase/)

![version](https://img.shields.io/badge/version-6.32.0-4668E2)
![stack](https://img.shields.io/badge/FastAPI%20·%20PostgreSQL%2016%20·%20React%2018-informational)
![deploy](https://img.shields.io/badge/Docker%20or%20bare--metal-2496ED)
![i18n](https://img.shields.io/badge/فارسی%20·%20English-00B0B1)
![source](https://img.shields.io/badge/source-proprietary%20·%20private-lightgrey)

</div>

---

## What Davam is

Davam is a web-based **CMMS/PMS** built to run maintenance operations for
drilling rigs. It replaces a foreign ERP system at an active drilling
contractor.

The system runs in production across three rigs and has grown over
**120 released versions** from a single login module into a full enterprise
platform — equipment hierarchy and work orders, official correspondence,
warehouse, procurement, HR workflows and management reporting.

> The source code is **private**. This page exists for the product overview
> and installation documentation only.

---

## A working day in Davam

The clearest explanation of Davam is to follow one real day:

**The night before**, the system generates tomorrow's work orders from the
PM schedules against the Jalali calendar. Nobody opens anything by hand.

**In the morning**, each technician opens "My desk" and sees only their own
work, on their own rig. Each task's checklist opens inline — for the daily
electrical checklist, say: inspect the generators, check load, the
switchboard room, VFD fans and filters, mud-pump motors. Every item takes
one of: done, not required, not done, needs parts, escalated to management.

**When work slips**, the system will not let it be closed without a
**delay reason**. That is the only thing keeping the overdue report honest
instead of turning everything green.

**When equipment fails**, the failure is logged with start and end time; the
system computes **downtime** itself and keeps the parts consumed, the fix
description and the preventive action. Those are what later produce MTBF
and MTTR.

**At the end of the day**, the daily report is generated from the PM tasks
themselves — grouped by department, with a count per status. The report is
**frozen at the moment it is filed** and does not change when tasks change
afterwards, because a signed report must not rewrite itself.

**At month end**, reports are archived into Jalali year and month folders
and can be handed over as a single ZIP or Excel file.

---

## What it does

### Maintenance — the core

| Area | Description |
|---|---|
| **Equipment tree** | Up to **six levels** (rig → system → equipment → sub-assembly → part), each with its technical code and model plus child counts. Importable from existing Excel files |
| **PM schedules** | Daily / weekly / monthly plans on the **Jalali calendar**, with nightly automatic work-order generation |
| **Work orders** | Full lifecycle with a unique number: issue, execute, inline checklist, close — with a mandatory delay reason on overdue work, and single or bulk duplication |
| **Failure reports** | Logged with automatic downtime calculation, parts consumed, fix description and preventive action, plus a resolved-failure history |
| **Unplanned work** | Outside the PM cycle, but inside the same reports |
| **Daily reports** | Generated from PM tasks per department, frozen when filed, archived in Jalali year/month folders, printable and ZIP output |

### Reporting and KPIs

The **KPI report** gives the standard maintenance indicators: **MTBF**,
**MTTR**, **Availability**, failure count, downtime hours and how many
assets failed — filterable by rig, department and period up to 12 months.

Fleet availability trend is drawn against colour thresholds
(green ≥98% · amber 95–98% · red below 95%), alongside monthly charts for
failure count and downtime hours.

**Excel export** is available from every list. The PM checklist export puts
each department on its own sheet, marks items with a tick or N/A, and
carries the due date and the delay reason. Ranges: today, current week,
current month, a custom range, all open work, or a full export — all on the
Jalali calendar.

### Supply chain

The purchasing pipeline is shown as **stages**, so it is visible exactly
where work is stuck: awaiting purchase, awaiting order approval, awaiting
receipt, awaiting invoice, invoice mismatch.

Material requests · purchase orders · receipt and inspection · invoice and
payment · suppliers · import files · stock on hand · goods in transit ·
stock cardex · item catalogue · repairable parts · warranty · cost ledger ·
budget · petty cash · FX rates — with a corporate warehouse API connector.

### Administration and HR

Official letters with letterhead, horizontal approval routing and scanned
signatures · inbox · document library · leave · travel requests · payslips ·
support tickets · multi-step approval engine with amount-based conditions.

### Platform

- **Bilingual** — Persian (RTL) and English (LTR), switchable at runtime,
  including printed and PDF output
- **Role-based access** — admin / manager / user, plus **per-rig data
  isolation**: a rig's users see only that rig's data
- **My desk and pending decisions** — every user knows exactly what is
  waiting on them
- **Branding** — company name and logos set from the panel itself, applied
  to the login screen, sidebar and letterheads (24 settings across 8 groups)
- **Nightly automatic backups** via `pg_dump`, with restore from the panel
- **Notifications** over Telegram, Bale and email
- **Assistant** for asking about equipment, work orders, failures, stock and
  letters in natural language — read-only; it never files or sends anything
- **Desktop shell** (Tauri) alongside the browser client and PWA

---

## Architecture

```
                        ┌──────────────┐
   Browser / desktop ──▶│  nginx (web) │  React 18 + TypeScript + Tailwind
                        └──────┬───────┘  RTL/LTR · Vazirmatn · Jalali dates
                               │ /api
                        ┌──────▼───────┐
                        │  FastAPI     │  37 modules · JWT · RBAC · APScheduler
                        └──────┬───────┘
                               │
                        ┌──────▼───────┐
                        │ PostgreSQL16 │  volumes: pgdata · uploads · backups
                        └──────────────┘
```

| Layer | Technology |
|---|---|
| Frontend | React 18, TypeScript, Tailwind CSS, Vite, Recharts |
| Backend | FastAPI, SQLAlchemy 2, Pydantic v2, APScheduler, PyJWT |
| Database | PostgreSQL 16 |
| Deployment | Docker Compose, or bare-metal on systemd + nginx |
| Desktop | Tauri |

---

## Requirements

| Item | Minimum | Notes |
|---|---|---|
| OS | Ubuntu 22.04 or 24.04 (64-bit) | The installer is tested on these two |
| CPU | 2 cores | Image build is the heaviest step |
| Memory | 2 GB | The current production install runs on exactly this |
| Disk | 20 GB free | Growth depends on attachments and backups |
| Access | `root` or `sudo` | |
| Network | Port 8080 open (or your chosen port) | Ports 80 and 443 for HTTPS |
| Internet | Required on the server | To fetch the package, images and libraries |

**Access token**: because the source is private, installation requires a
read-only token. Request one from the Davam team.

---

## Installation

Installation runs entirely **through the GitHub API** — no manual file upload.
Two installation methods are available, both driven by a single script.

### Step 1 — fetch the installer

```bash
export DAVAM_GH_TOKEN='your-token-here'

curl -fsSL \
  -H "Authorization: Bearer $DAVAM_GH_TOKEN" \
  -H "Accept: application/vnd.github.raw" \
  https://api.github.com/repos/m0000hamad/davam/contents/davam.sh \
  -o davam.sh
```

### Step 2 — run the menu

```bash
bash davam.sh
```

Pick option 1 (Docker) or 2 (bare-metal). The script installs the
prerequisites itself, pulls the latest release from GitHub, generates a
**random** database password and secret key, configures the firewall, and
finishes with an acceptance check.

### Which method?

| | **Docker** (recommended) | **Bare-metal** |
|---|---|---|
| Isolation | Full — three separate containers | Runs on the host OS |
| Extra prerequisite | Docker | PostgreSQL, Python, nginx from apt |
| Node on the server | Not required | Not required¹ |
| Adminer (browser DB admin) | ✅ | ❌ |
| Best for | Most cases | Servers where Docker is not permitted |

<sub>¹ Release packages ship a pre-built frontend.</sub>

### Unattended install

```bash
DAVAM_GH_TOKEN='…' bash davam.sh install-docker    # or install-direct
```

### After installation

The URL, username and initial password are printed at the end.
**Change the admin password immediately after the first login.**

Optional next steps:

```bash
bash davam.sh ssl example.com you@mail.com   # domain and HTTPS
bash davam.sh autobackup                     # nightly backups
bash davam.sh agent-install                  # enable in-app updates
```

---

## Updating

Data survives every method: the database, attachments and the `.env` file are
never overwritten, and **a backup is taken automatically before every update**.

### 1) From inside the application

**Settings → System update**. The page shows the new version, expands the
changelog, and installs with one click. Enable it once on the server:

```bash
bash davam.sh agent-install
```

> The backend deliberately never touches the server itself: it only records a
> *request*, and an agent running on the host carries it out. If the API could
> reach Docker or systemd, any API compromise would become root access.

### 2) From the menu

```bash
bash davam.sh
```
Option 4 (latest) or 5 (specific version).

### 3) From the command line

```bash
bash davam.sh check            # only report what is new
bash davam.sh update           # latest version
bash davam.sh update 6.31.0    # a specific version
bash davam.sh changes 6.30.0   # what changed since that version
```

The script detects whether the install is Docker or bare-metal on its own.
When it finishes, it prints **the changelog for every version it skipped over**.

### Per-customer channels

Each installation can follow its own update channel (in `.env`):

```ini
UPDATE_CHANNEL=stable        # public releases only
UPDATE_CHANNEL=<customer>    # customer-specific releases take priority
UPDATE_PIN=6.31.0            # ceiling — never go above this version
```

---

## Day-to-day operations

```bash
bash davam.sh status            # services, version, disk space
bash davam.sh logs api          # backend logs
bash davam.sh backup            # immediate backup
bash davam.sh autobackup 3      # nightly backup at 03:00
bash davam.sh dbadmin           # Adminer on port 5050
bash davam.sh uninstall         # complete removal ⚠️
```

---

## Security

- The database password and `SECRET_KEY` are generated **randomly per
  installation** — no default value ever reaches production.
- JWT authentication with bcrypt password hashing.
- Role-based access control plus per-rig data isolation.
- Audit log for sensitive operations.
- The backend listens on an internal port only; external traffic goes
  through nginx.
- The repository token is **read-only** and scoped to a single repository.
- HTTPS via Let's Encrypt in one command.

---

## Source access

The code repository is **private** and access is granted by invitation only.
If you need the source for evaluation, audit or collaboration, get in touch.

## Support

- Something broken? Send the output of `bash davam.sh status` and
  `bash davam.sh logs api` with your report.
- The complete per-version changelog ships inside the package as
  `CHANGELOG.md`.

---

<div align="center">
<sub>Davam — proprietary software. All rights reserved.</sub>
</div>
