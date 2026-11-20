# DCEMS — Data Center Environmental Monitoring System

[![Status](https://img.shields.io/badge/status-bootstrapped-green)](.) 
[![Backend](https://img.shields.io/badge/backend-.NET%2010%20LTS-blue.svg)](.)
[![Frontend](https://img.shields.io/badge/frontend-React%2BTypeScript-emerald.svg)](.)
[![Database](https://img.shields.io/badge/database-PostgreSQL-success.svg)](.)

> **Data Center Environmental Monitoring System** — Aplikasi monitoring suhu dan kelembapan ruang data center melalui sensor yang terhubung menggunakan USB Serial.

---

## 📋 Table of Contents

- [About Project](#about-project)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Development Roadmap](#development-roadmap)
- [Status & Implementation](#status--implementation)
- [Configuration (Sensor Settings)](#configuration-sensor-settings)
- [Documentation](#documentation)
- [Getting Started](#getting-started)

---

## About Project

DCEMS adalah aplikasi monitoring real-time untuk **suhu dan kelembapan ruang data center**. Sistem ini terhubung dengan sensor via USB Serial untuk collect environmental data secara continuous, menampilkan dashboard interaktif, mengirim alert notification melalui email Microsoft 365, dan menghasilkan daily snapshot report.

### Target Users
- **Data Center Operators** — Monitoring kondisi lingkungan real-time
- **System Administrators** — Manage configuration dan user accounts
- **IT Stakeholders** — View historical data dan reports via dashboard

### Why DCEMS?
- ✅ **Real-time Monitoring** — Dashboard dengan live charts via SignalR WebSocket
- ✅ **Alert Notifications** — Email alerts via Microsoft Graph API saat threshold exceeded
- ✅ **Historical Data** — PostgreSQL untuk time-series storage dan analysis
- ✅ **Daily Reports** — Automatic snapshot pada 09:00 WITA untuk reporting
- ✅ **Secure LAN Access** — Access via intranet untuk security

---

## Features

Berikut adalah fitur-fitur yang direncanakan untuk DCEMS:

### Core Monitoring Features ⏸️ (To Be Implemented)

| Feature | Description | Status |
|---------|-------------|--------|
| Real-time Dashboard | Live temperature & humidity charts via SignalR | NOT IMPLEMENTED |
| Sensor Data Ingestion | USB Serial COM port data parsing | NOT IMPLEMENTED |
| Historical Data Storage | PostgreSQL time-series database | NOT IMPLEMENTED |
| Alert System | Threshold-based email notifications (Microsoft 365) | NOT IMPLEMENTED |
| Daily Snapshot Report | Automatic report generation pada 09:00 WITA | NOT IMPLEMENTED |
| User Management | Role-based access control (Admin, Operator, Viewer) | NOT IMPLEMENTED |

### Configuration Features ⏸️ (To Be Implemented)

| Feature | Description | Status |
|---------|-------------|--------|
| Serial Port Config | Configure COM port, baud rate, data format | NOT IMPLEMENTED |
| Alert Threshold Settings | Set temperature/humidity thresholds per zone | NOT IMPLEMENTED |
| Email Recipients Management | Configure notification recipients | NOT IMPLEMENTED |
| Sensor Management | Add/remove sensors via UI | NOT IMPLEMENTED |

### System Features

| Feature | Description | Status |
|---------|-------------|--------|
| Health Check Endpoint | `/api/v1/health` for load balancing | PLANNED |
| SSL/TLS Encryption | HTTPS for all API communication | PLANNED |
| Audit Trail | Alert log untuk compliance | PLANNED |

---

## Technology Stack

### Backend ⏸️ (Not Yet Implemented)
- **Runtime:** [.NET 10 LTS](https://learn.microsoft.com/dotnet/core/) — Enterprise-ready, production-grade
- **Framework:** [ASP.NET Core Web API](https://learn.microsoft.com/aspnet/core/) — RESTful API dengan high performance
- **Worker Service:** [.NET Worker Service](https://learn.microsoft.com/dotnet/core/extend/worker-services) — Background processing untuk serial data & periodic sampling
- **ORM:** [Entity Framework Core](https://learn.microsoft.com/ef/) — Database ORM dengan migrations support

### Frontend ⏸️ (Not Yet Implemented)
- **Framework:** [React 18+](https://react.dev/) — UI framework dengan component-based architecture
- **Language:** [TypeScript](https://www.typescriptlang.org/) — Type-safe development
- **Build Tool:** [Vite](https://vitejs.dev/) — Fast development server dengan hot module replacement
- **Styling:** [Tailwind CSS](https://tailwindcss.com/) — Utility-first CSS framework
- **Charts:** [Recharts](https://recharts.org/) — Data visualization library
- **Realtime:** [SignalR Client](https://learn.microsoft.com/dotnet/aspnet/signalr/client) — WebSocket connection untuk real-time updates

### Database
- **Engine:** [PostgreSQL 15+](https://www.postgresql.org/) — ACID compliant, excellent time-series support
- **ORM Provider:** [Npgsql](https://www.npgsql.org/) — PostgreSQL driver for .NET

### External Services
- **Email Notification:** [Microsoft Graph API](https://learn.microsoft.com/graph/) — Secure OAuth2 authentication untuk send email ke Microsoft 365 tenants
- **Version Control:** Git

### Deployment (TBD)
- **Option A:** IIS + Static Files (recommended for LAN production)
- **Option B:** Docker Compose (development/staging)
- **Option C:** Azure App Service (cloud with LAN access)

**Note:** Deployment strategy masih TBD. Lihat [`docs/DEPLOYMENT.md`](docs/DEPLOYMENT.md) untuk detail.

---

## Project Structure

```
monitoring-suhu-drc/
├── .agent/                          ← Agent memory (WAJIB dibaca!)
│   ├── PROJECT_RULES.md            ← Aturan wajib untuk semua agen
│   ├── PROJECT_STATE.md            ← Status terkini proyek ⭐ START HERE
│   ├── TASKS.md                    ← Roadmap lengkap dengan milestones
│   ├── DECISIONS.md                ← Keputusan teknis yang sudah diambil
│   ├── HANDOFF.md                  ← Panduan handoff ke agen berikutnya
│   ├── ARCHITECTURE.md             ← Arsitektur sistem overview
│   └── KNOWN_ISSUES.md             ← Masalah & limitations yang diketahui
│
├── docs/                            ← Technical documentation
│   ├── SRS.md                      ← Software Requirements Specification
│   ├── ERD.md                      ← Entity Relationship Diagram
│   ├── API_SPEC.md                 ← REST API specification
│   ├── DATABASE_DESIGN.md          ← Database schema detail
│   ├── DEPLOYMENT.md               ← Deployment guide
│   └── TEST_PLAN.md                ← Testing plan & strategies
│
├── src/                             ← Source code (BELUM ADA)
│   ├── DCEMS.API/                   ← .NET Web API project
│   ├── DCEMS.Worker/               ← .NET Worker Service project
│   └── DCEMS-Frontend/             ← React TypeScript SPA (belum dibuat)
│
├── tests/                           ← Test files (BELUM ADA)
│   ├── unit/                       ← Unit test cases (.NET + React)
│   └── integration/                ← Integration & E2E tests
│
├── database/                        ← Database scripts
│   └── migrations/                 ← EF Core migrations / SQL scripts
│
└── deployment/                      ← Deployment configurations
    ├── iis/                        ← IIS hosting configs (if Option A)
    └── docker/                    ← Dockerfiles & compose.yml (if Option B/C)
```

**Legend:**
- ⭐ — **START HERE!** Baca file ini dulu untuk memahami status proyek
- 📖 — Documentation files (read-only, no code in here yet)
- 🔒 — Agent memory yang harus dibaca sebelum kerja (WAJIB!)

---

## Development Roadmap

Lihat [`TASKS.md`](.agent/TASKS.md) untuk detail roadmap lengkap.

### Current Phase: Bootstrap & Documentation ✅

**Status:** SELESAI  
**Tanggal Selesai:** 2026-11-20

#### What's Been Completed
- [x] Struktur folder proyek dibuat (.agent/, docs/, src/, tests/, database/, deployment/)
- [x] Dokumentasi agent memory (7 files) untuk governance
- [x] Technical documentation (6 files) untuk referensi teknis
- [x] README.md ini dengan informasi proyek lengkap
- [x] .gitignore untuk .NET + Node.js + React environment
- [x] Git repository sudah terinisialisasi

#### What's Next
**TASK 01: Technical Design Deep Dive** — Konfirmasi hardware, detail spesifikasi, finalisasi architecture.

Lihat [`.agent/TASKS.md`](.agent/TASKS.md) untuk roadmap lengkap dengan semua task phases.

---

## Status & Implementation

### ⚠️ IMPORTANT: Project Is Still In Bootstrap Phase!

Proyek DCEMS **masih dalam tahap bootstrap/dokumentasi**. Belum ada:
- ❌ Source code yang diimplementasikan (folder `src/` masih kosong)
- ❌ Database schema yang dibuat (belum ada PostgreSQL database)
- ❌ Dependency packages yang diinstal (belum ada NuGet/npm packages)
- ❌ Testing yang dilakukan (no test results yet)
- ❌ Deployment ke production

**Semua dokumentasi adalah rancangan awal (TBD/To Be Determined)** dan perlu dikonfirmasi sebelum implementasi!

### Implementation Checklist

| Component | Status | Notes |
|-----------|--------|-------|
| Bootstrap & Documentation | ✅ DONE | Folder + docs created |
| Technical Design Deep Dive | ⏸️ TBD | Hardware verification needed |
| Backend Development | ❌ NOT STARTED | Source code belum ada |
| Frontend Development | ❌ NOT STARTED | React app belum dibuat |
| Database Setup | ❌ NOT STARTED | PostgreSQL belum setup |
| Integration Testing | ❌ NOT STARTED | Belum ada testing |
| Deployment | ❌ NOT STARTED | Belum deploy ke production |

---

## Configuration (Sensor Settings) ⚠️ PERLU DIVERIFIKASI

Konfigurasi sensor berikut masih **belum diverifikasi** terhadap perangkat fisik! Semua nilai di bawah adalah asumsi yang perlu dikonfirmasi.

### Serial Port Configuration

| Parameter | Value | Status |
|-----------|-------|--------|
| **Port** | COM3 | ⚠️ PERLU KONFIRMASI |
| **Baud Rate** | 9600 | ⚠️ PERLU KONFIRMASI |
| **Data Bits** | 8 | TBD |
| **Parity** | None (No parity) | TBD |
| **Stop Bits** | 1 | TBD |
| **Handshake** | None | TBD |

### Data Format Assumption

```
*A<Temperature>°C#*B<Humidity>%#
Contoh: *A25.50#*B60.90#
- A: Temperature dalam °C (float)
- B: Humidity dalam % (float)
```

**⚠️ PENTING:** Format data ini adalah asumsi! Perlu verifikasi terhadap dokumentasi sensor yang sebenarnya sebelum deployment!

### Sampling Configuration

| Parameter | Value | Status |
|-----------|-------|--------|
| Target Sampling Interval | 10 detik per sensor | TBD |
| Daily Snapshot Time | 09:00 WITA (UTC+8) | ✅ Dikonfirmasi |

---

## Documentation

Dokumentasi proyek terstruktur menjadi dua kategori:

### Agent Memory Files (WAJIB dibaca sebelum kerja!)
Lokasi: `.agent/`

- [`PROJECT_RULES.md`](.agent/PROJECT_RULES.md) — Aturan wajib untuk semua agen 🚨
- [`PROJECT_STATE.md`](.agent/PROJECT_STATE.md) — Status terkini proyek ⭐ START HERE
- [`TASKS.md`](.agent/TASKS.md) — Roadmap lengkap dengan milestones
- [`DECISIONS.md`](.agent/DECISIONS.md) — Keputusan teknis yang sudah diambil
- [`HANDOFF.md`](.agent/HANDOFF.md) — Panduan handoff ke agen berikutnya
- [`ARCHITECTURE.md`](.agent/ARCHITECTURE.md) — Arsitektur sistem overview
- [`KNOWN_ISSUES.md`](.agent/KNOWN_ISSUES.md) — Masalah & limitations yang diketahui

### Technical Documentation
Lokasi: `docs/`

- [`SRS.md`](docs/SRS.md) — Software Requirements Specification
- [`ERD.md`](docs/ERD.md) — Entity Relationship Diagram untuk database design
- [`API_SPEC.md`](docs/API_SPEC.md) — REST API specification dengan examples
- [`DATABASE_DESIGN.md`](docs/DATABASE_DESIGN.md) — Database schema detail
- [`DEPLOYMENT.md`](docs/DEPLOYMENT.md) — Deployment guide step-by-step
- [`TEST_PLAN.md`](docs/TEST_PLAN.md) — Testing plan & strategies

---

## Getting Started

### Prerequisites

Untuk memulai development DCEMS, pastikan Anda memiliki:

- [.NET 10 LTS SDK](https://learn.microsoft.com/dotnet/core/install/) (untuk backend)
- [Node.js 18+](https://nodejs.org/) (untuk frontend)
- [PostgreSQL 15+](https://www.postgresql.org/download/) (database server)
- Git

### Clone Repository

```bash
git clone <repository-url>
cd monitoring-suhu-drc
```

### Read Documentation First 📖

**PENTING:** Sebelum mulai coding, baca dokumentasi berikut:

1. [`PROJECT_STATE.md`](.agent/PROJECT_STATE.md) — Pahami status proyek saat ini
2. [`ARCHITECTURE.md`](.agent/ARCHITECTURE.md) — Pahami arsitektur sistem
3. [`TASKS.md`](.agent/TASKS.md) — Lihat roadmap dan task yang perlu dikerjakan
4. `.agent/KNOWN_ISSUES.md` — Pelajari masalah yang perlu diperhatikan

### Verify Hardware Configuration ⚠️

Sebelum development dimulai, verifikasi konfigurasi sensor:

```powershell
# Check if COM3 exists
Get-PnpDevice | Where-Object {$_.FriendlyName -like "*USB*Serial*" -or $_.InstanceId -like "PORTS\VID_XXXX&PID_XXXX&REV_*"} | Select-Object Name, Status, FriendlyName
```

Lihat `.agent/DECISIONS.md` untuk detail hardware verification steps.

### Run Development Server (After Implementation)

Setelah source code diimplementasikan:

#### Backend (.NET API + Worker)

```bash
cd src/DCEMS.API
dotnet restore
dotnet run

# Or for production-ready build:
dotnet publish -c Release -o ../publish/
```

#### Frontend (React SPA)

```bash
cd src/DCEMS-Frontend
npm install
npm run dev

# Or build for production:
npm run build
```

---

## Contributing

Proyek ini masih dalam tahap bootstrap. Untuk kontribusi:

1. **Baca `.agent/PROJECT_RULES.md`** — Pahami aturan wajib
2. **Review `.agent/PROJECT_STATE.md`** — Cek status terkini
3. **Buat issue untuk task baru** — Sebelum mulai implementasi
4. **Ikuti roadmap di `.agent/TASKS.md`** — Jangan skip phases!

---

## License & Security

### Security Considerations

- Aplikasi hanya diakses via **LAN/intranet** (tidak ke public internet)
- Semua API communication akan menggunakan **HTTPS/TLS** di production
- User credentials disimpan dengan **password hashing** (bcrypt/argon2)

Jika Anda menemukan vulnerability, laporkan melalui [responsibility disclosure channel](TBD).

---

## Support & Contact

Untuk pertanyaan mengenai proyek ini:

- Technical Lead: TBD
- Development Team Email: TBD

---

## Quick Links

- [Project Rules](.agent/PROJECT_RULES.md) 🚨 — **Baca dulu sebelum kerja!**
- [Project State](.agent/PROJECT_STATE.md) ⭐ — Status terkini (START HERE!)
- [Architecture Overview](.agent/ARCHITECTURE.md) — Sistem architecture
- [Known Issues](.agent/KNOWN_ISSUES.md) — Masalah yang perlu diperhatikan

---

## Version History

| Version | Date | Changes | Status |
|---------|------|---------|--------|
| 0.0.1-alpha | 2026-11-20 | Bootstrap & documentation complete | ✅ RELEASED (DOCS ONLY) |

---

**Last Updated:** 2026-11-20  
**Maintained By:** DCEMS Development Team  

> 📌 **Remember:** This project is still in bootstrap mode! No source code exists yet. All documentation is draft/TBD until verified by stakeholders and technical review.
