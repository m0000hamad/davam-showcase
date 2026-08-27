<div align="center">

# Davam

**Integrated Industrial Maintenance Management System**

[فارسی](README.md) · English · [Landing page](https://m0000hamad.github.io/davam-showcase/)

![version](https://img.shields.io/badge/version-6.35.0-4668E2)
![stack](https://img.shields.io/badge/FastAPI%20·%20PostgreSQL%2016%20·%20React%2018-informational)
![deploy](https://img.shields.io/badge/Docker%20or%20bare--metal-2496ED)
![i18n](https://img.shields.io/badge/فارسی%20·%20English-00B0B1)
![source](https://img.shields.io/badge/source-proprietary%20·%20private-lightgrey)

</div>

---

## What Davam is

Davam is a web-based **CMMS/PMS** for any organisation that owns physical
assets and has to keep them running — a factory, a production line, a power
plant, a fleet, a refinery or a drilling rig.

Nothing in its logic is tied to one industry: **asset, maintenance plan,
work order, failure, part and indicator** mean the same thing wherever
maintenance is done. What sets Davam apart is that it implements those
concepts with real discipline rather than as empty forms.

The system was **hardened in an unforgiving environment** — drilling, where
equipment downtime converts directly into daily cost. It runs in production
across three sites today and has grown over **123 released versions** from a
single login module into a full enterprise platform: equipment hierarchy and
work orders, official correspondence, warehouse, procurement, HR workflows
and management reporting. It replaced a foreign ERP system and does the same
job on the Jalali calendar and in Persian.

> **One honest note:** the current build carries drilling vocabulary — the
> unit that separates assets is called a *rig*. Deploying into another
> industry means setting that label to whatever fits ("plant", "site",
> "line"); the underlying structure and logic do not change.

> The source code is **private**. This page exists for the product overview
> and installation documentation only.

---

## Screens

| | |
|---|---|
| ![Management dashboard](assets/screenshots/admin-dashboard.png) | ![Equipment tree](assets/screenshots/equipment-tree.png) |
| **Management dashboard** — open and overdue work, PM progress per rig | **Equipment tree** — up to six levels, with each item's code and model |
| ![KPI report](assets/screenshots/kpi.png) | ![Failure report](assets/screenshots/failure-report.png) |
| **KPI report** — MTBF, MTTR and availability, with a 12-month trend | **Failure report** — downtime, parts consumed, fix and prevention |
| ![Daily report](assets/screenshots/daily-report-generate.png) | ![PM tasks](assets/screenshots/pm-tasks.png) |
| **Building the daily report** — from the PM tasks themselves, per department | **PM tasks** — the technician's desk, with Excel export |

<sub>More screens on the [landing page](https://m0000hamad.github.io/davam-showcase/).</sub>

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

### 🛠 Maintenance — the core

**🌳 A precise asset register.** Equipment is modelled as a deep hierarchy —
from the rig down to the smallest replaceable part — and every item carries
its own technical code, model and history. An organisation's existing
structure is bulk-imported from Excel, so going live does not mean typing in
thousands of records by hand.

**📅 Preventive maintenance planning on the Jalali calendar.** Daily, weekly
and monthly cycles are defined once, and the system **generates the next
day's work orders every night by itself**. Plans and their checklists are
importable, editable and resettable from a file.

**🔧 The complete work-order lifecycle.** Every job gets a unique number, its
execution checklist opens inline, and each line takes a precise status —
from "done" through "needs parts" to "escalated to management". Bulk creation
and duplication are supported for recurring programmes.

**⛔ Delay discipline — the feature that keeps reporting honest.** Overdue
work **cannot be closed without recording a delay reason**. It is the single
control that stops a monthly report from becoming a meaningless wall of green.

**⚠️ Failure and downtime management.** Failures are logged with start and end
time and **downtime is computed automatically**. Parts consumed, the fix and
the preventive action are retained — exactly the data that later turns into
reliability indicators with no human transcription. Unplanned work has its
own route but lands in the same reports.

**📄 A daily report that writes itself.** The report is generated from the
completed work, split by department, and **frozen the moment it is filed** —
because a signed report must not rewrite itself when tasks change later.
Structured monthly archiving and single-file handover are built in.

### 📊 Reporting and KPIs

**📈 Standard reliability indicators.** The system computes **MTBF**,
**MTTR** and **availability** alongside failure counts, downtime hours and
the number of assets involved — breakable down by rig, department and period
up to a full year. None of it is typed in; it all falls out of the day-to-day
failure logging.

**🚦 Early warning through banded thresholds.** Fleet availability is plotted
against defined bands, so a decline is visible **before it becomes critical**,
not after.

**📗 Professional Excel output from any list.** The maintenance checklist
export lays each department out on its own sheet, marks the status of every
line and carries the due date and delay reason. The period is fully flexible —
from a single day to a complete export — all on the Jalali calendar.

### 📦 Supply chain — from need to settlement

**🧾 Advanced material requisition with precise tracking.** Every request is
traceable from the moment it is raised until the goods arrive, and at any
point it is clear whose desk it is sitting on. Approval routing is
multi-stage and **amount-aware**: small purchases take a shorter path, and
financial sign-off is only required above a defined ceiling.

**🔎 Bottleneck detection, not just order entry.** The purchasing pipeline is
presented as sequential stages that point directly at where work has actually
stalled — awaiting purchase, approval, receipt or invoice. Management does
not have to go hunting for someone.

**⚖️ Three-way matching.** Order, goods receipt and invoice are reconciled
against each other and mismatches are flagged automatically; open commitment
converts into confirmed cost once the amount is approved, and lands in the
cost ledger.

**🏬 Inventory with a complete movement history.** Multi-warehouse stock,
goods in transit and a full per-item movement ledger are maintained.
Repairable and warrantied items follow their own path, and parts consumption
links straight back to the maintenance cost of the specific asset.

**💱 Financial and budget control** with multi-currency support and
configurable rates, plus per-rig petty cash. The system also integrates with
the corporate central warehouse, so data need not be kept in two places.

### ✉️ Administration and HR — the paperwork, without paper

**📜 Full official correspondence.** Letters are composed on the
organisation's official letterhead, numbered automatically, routed for
approval and stamped with the signer's scanned signature. Internal and
external recipients, carbon copies, attachments, confidentiality level and
urgency are all supported; the inbox tracks read and action status. The final
output is print- and archive-ready.

**🗂 An organised document archive** with categorisation and search, so
technical and administrative records live in one defined place instead of in
people's mailboxes.

**👥 HR processes** — leave, missions and travel, payslips and internal
support — all run on **one shared workflow engine**. Approval rules are
defined once and every process obeys them; adding a new process does not mean
rewriting approval logic.

**⚙️ A configurable approval engine** that resolves stages by role,
department, direct manager or amount threshold, applies response deadlines,
and skips unnecessary steps on its own.

### 🧩 Platform and experience

**🌐 Genuine bilingualism, not a surface translation.** Persian (RTL) and
English (LTR) switch instantly — and crucially the page direction, calendar,
number formatting and even **printed and PDF output** switch with the language.

**🔐 Layered access with data isolation.** Beyond organisational roles, data
is **isolated per rig**: a rig's users see only that rig's data, and a
multi-rig manager sees only the rigs they supervise. Access to each area is
independently controllable.

**📥 A personal desk and decision queue.** Every user sees at a glance what is
waiting on them, without hunting through sections.

**🎨 Complete white-labelling.** Company name and logos, system colours, the
login screen and letterheads are all set from inside the panel. The system
comes up wearing each organisation's identity rather than a fixed skin.

**💾 Nightly automatic backups with in-panel restore.** Retention depth is
configurable and restoring needs no server access.

**🔔 Multi-channel notifications** over messaging platforms and email, so work
does not stall behind an approval.

**🤖 An intelligent assistant** that answers natural-language questions such as
"how many work orders are open?" or "what is the status of mud pump 1?". It is
deliberately **read-only** — it never files or sends anything.

**📱 On mobile and desktop.** Beyond the browser it installs as a mobile app,
and a standalone desktop build is available.

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

**Access token**: because the release repository is private, installation
requires a read-only token, supplied with the install command. It is
unrelated to the product licence — the licence governs *use*, the token only
permits *fetching the package*.

On the server the token lives at `/etc/davam/token` with mode `600` owned by
`root`, not in `.env` — because `.env` is also read by the application
container, and the token should not be reachable by a process that answers
requests from the network.

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
