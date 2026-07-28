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

Create `backend/.env` based on the table below:

| Variable | Description |
|----------|-------------|
| `PORT` | Server port (default: 5000) |
| `DATABASE_URL` | SQLite path, e.g. `file:./dev.db` |
| `JWT_SECRET` | Secret key for JWT signing |
| `JWT_EXPIRES_IN` | Token expiry, e.g. `7d` |
| `AWS_REGION` | AWS region for Bedrock |
| `AWS_ACCESS_KEY_ID` | AWS access key |
| `AWS_SECRET_ACCESS_KEY` | AWS secret key |
| `BEDROCK_MODEL_ID` | Bedrock inference profile ARN |
| `SMTP_HOST` | SMTP server host |
| `SMTP_PORT` | SMTP port (587) |
| `SMTP_USER` | SMTP username/email |
| `SMTP_PASS` | SMTP password / app password |
| `JIRA_BASE_URL` | Jira workspace URL |
| `JIRA_ADMIN_EMAIL` | Jira admin email |
| `JIRA_API_TOKEN` | Jira API token |
| `JIRA_PROJECT_KEY` | Jira project key |

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
