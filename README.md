# Performance Management System (PMS)

A full-stack Performance Management System built for a hackathon, featuring goal tracking, AI-powered reviews, leave management, Jira integration, and role-based dashboards.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 19, Vite, Tailwind CSS, React Router |
| Backend | Node.js, Express 5 |
| Database | SQLite (via Prisma ORM) |
| AI | AWS Bedrock (Claude) |
| Integrations | Jira Cloud API, Nodemailer (SMTP) |
| Auth | JWT + bcrypt |

## Features

- **Role-based access** — Employee, Manager, HR dashboards
- **Goal Management** — Create, approve/reject, track progress with Jira sync
- **AI Reviews** — Auto-generated performance summaries via AWS Bedrock
- **Leave & WFH Requests** — Submit and approve leave requests
- **Notifications** — In-app notification system
- **Reports & Analytics** — PDF reports, HR analytics
- **Timeline** — Activity timeline per employee

## Project Structure

```
Hackathon/
├── backend/
│   ├── prisma/          # Schema, migrations, seed
│   ├── src/
│   │   ├── controllers/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── middleware/
│   │   └── config/
│   └── package.json
└── frontend/
    ├── src/
    │   ├── pages/       # employee / manager / hr
    │   ├── components/
    │   ├── api/
    │   └── context/
    └── package.json
```

## Getting Started

### Prerequisites
- Node.js >= 18
- npm

### Backend Setup

```bash
cd backend
npm install
cp .env.example .env   # fill in your values
npx prisma migrate dev
npm run seed
npm run dev            # runs on http://localhost:5000
```

### Frontend Setup

```bash
cd frontend
npm install
npm run dev            # runs on http://localhost:5173
```

## Environment Variables

Create `backend/.env` using the template below and fill in your values:

```env
# ── Server ────────────────────────────────────────
PORT=5000
NODE_ENV=development

# ── Database ──────────────────────────────────────
# SQLite (default). For PostgreSQL use: postgresql://user:pass@localhost:5432/dbname
DATABASE_URL="file:./dev.db"

# ── Auth ──────────────────────────────────────────
JWT_SECRET=your_strong_secret_key_here
JWT_EXPIRES_IN=7d

# ── AWS Bedrock (AI Reviews) ──────────────────────
# IAM user must have: bedrock:InvokeModel permission
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your_aws_access_key_id
AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key
# Model ID or full cross-region inference profile ARN
# e.g. arn:aws:bedrock:us-east-1:<account_id>:application-inference-profile/<id>
BEDROCK_MODEL_ID=your_bedrock_model_id_or_arn

# ── SMTP Email (Nodemailer) ────────────────────────
# Gmail: generate an App Password from Google Account > Security > App Passwords
# App Password format: "xxxx xxxx xxxx xxxx" (16 chars with spaces)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_gmail_app_password
SMTP_FROM="Performance Management System <your_email@gmail.com>"

# ── Jira Integration ──────────────────────────────
# Workspace URL — no trailing slash
JIRA_BASE_URL=https://your-domain.atlassian.net
# Admin account used for all Jira API calls (needs "Administer Jira" permission)
JIRA_ADMIN_EMAIL=jira_admin@example.com
# Generate at: Atlassian Account > Security > API tokens
JIRA_API_TOKEN=your_jira_api_token
# Jira project key where goals are created as Tasks
JIRA_PROJECT_KEY=PMS
```

> **Never commit `.env` to version control.** It is already covered by `.gitignore`.

## Default Roles

After seeding, the following roles are available:
- **HR** — Manage users, view analytics, oversee all goals/reviews
- **Manager** — Approve goals, manage team, handle leave requests
- **Employee** — Set goals, track progress, request leave

## Scripts

### Backend
| Command | Description |
|---------|-------------|
| `npm run dev` | Start with nodemon |
| `npm run seed` | Seed the database |
| `npm run prisma:studio` | Open Prisma Studio |
| `npm run prisma:migrate` | Run migrations |

### Frontend
| Command | Description |
|---------|-------------|
| `npm run dev` | Start dev server |
| `npm run build` | Production build |
| `npm run lint` | Run ESLint |
