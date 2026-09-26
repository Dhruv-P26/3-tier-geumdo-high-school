# Geumdo High School — 3-Tier Web Application

A 3-tier school management website built as a final year project:

- **Tier 1 — Presentation:** static HTML/CSS/JS, served by Nginx (`frontend/`)
- **Tier 2 — Application/API:** Node.js + Express REST API (`backend/`)
- **Tier 3 — Database:** MySQL 8 (`database/init.sql`)

## Folder structure (where every file lives)

```
geumdo-school/
├── docker-compose.yml          # wires all 3 tiers together
├── .gitlab-ci.yml               # auto-deploy pipeline (push -> EC2)
├── README.md
│
├── frontend/                    # TIER 1
│   ├── Dockerfile
│   ├── nginx.conf                # proxies /api/* to the backend container
│   ├── index.html                 (Home)
│   ├── about.html                 (About Us)
│   ├── activities.html            (Activities)
│   ├── contact.html               (Contact Us)
│   ├── student-portal.html        (Student Portal)
│   ├── faculty.html               (Faculty & Staff)
│   ├── css/style.css
│   └── js/main.js
│
├── backend/                     # TIER 2
│   ├── Dockerfile
│   ├── package.json
│   ├── .env.example
│   ├── server.js
│   ├── db.js
│   └── routes/
│       ├── faculty.js
│       ├── activities.js
│       ├── notices.js
│       ├── contact.js
│       └── students.js
│
└── database/                    # TIER 3
    └── init.sql                  # schema + seed data, auto-run on first MySQL boot
```

## Run it locally (test before you deploy)

Requires Docker + Docker Compose installed.

```bash
cd geumdo-school
docker compose up -d --build
```

Then open **http://localhost** in your browser. The API lives at `http://localhost/api/...` (proxied through Nginx to the backend container).

To stop everything:
```bash
docker compose down          # keeps the database volume (data persists)
docker compose down -v       # also wipes the database volume (fresh start)
```

## Demo Student Portal login
- Student ID: `GHS-2026-014`
- Password: `geumdo123`

(Seeded in `database/init.sql` — add more rows there for more demo accounts.)

## Before you submit / present this project
1. **Replace the placeholder photos.** Every `<img>` currently points at `picsum.photos` (randomly generated placeholder images) because copyrighted TV/movie stills can't be used here. Take or source your own licensed photos of a real school (or your own campus) and swap the URLs in the HTML files with your own images in `frontend/images/`.
2. Change the default database passwords in `docker-compose.yml` before deploying anywhere public.
3. See the accompanying **AWS Deployment Guide (PDF)** for full VPC → EC2 → Docker → Load Balancer → GitLab CI/CD deployment steps written for a first-time DevOps fresher.
