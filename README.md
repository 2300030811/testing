# MockMate

MockMate is a full-stack interview and career prep platform built with Next.js 14.
It combines certification practice, AI interview simulation, resume tooling,
career tracking, and engineering challenge modes in one codebase.

Live demo: https://mockmate-delta.vercel.app/

## Table of Contents

- [Tech Icons](#tech-icons)
- [What Is Implemented](#what-is-implemented)
- [Current Route Map](#current-route-map)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Scripts](#scripts)
- [Career Ops Runbook](#career-ops-runbook)
- [Security and Reliability](#security-and-reliability)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [Team](#team)
- [License](#license)

## Tech Icons

<p>
  <img src="https://cdn.simpleicons.org/nextdotjs" alt="Next.js" height="30" />
  <img src="https://cdn.simpleicons.org/react" alt="React" height="30" />
  <img src="https://cdn.simpleicons.org/typescript" alt="TypeScript" height="30" />
  <img src="https://cdn.simpleicons.org/tailwindcss" alt="Tailwind CSS" height="30" />
  <img src="https://cdn.simpleicons.org/framer" alt="Framer Motion" height="30" />
  <img src="https://cdn.simpleicons.org/supabase" alt="Supabase" height="30" />
  <img src="https://cdn.simpleicons.org/postgresql" alt="PostgreSQL" height="30" />
  <img src="https://cdn.simpleicons.org/redis" alt="Redis" height="30" />
  <img src="https://cdn.simpleicons.org/vercel" alt="Vercel" height="30" />
</p>

<p>
  <img src="https://cdn.simpleicons.org/google" alt="Google Gemini" height="30" />
  <img src="https://cdn.simpleicons.org/groq" alt="Groq" height="30" />
  <img src="https://cdn.simpleicons.org/openai" alt="OpenAI" height="30" />
  <img src="https://cdn.simpleicons.org/microsoftazure" alt="Azure" height="30" />
  <img src="https://cdn.simpleicons.org/playwright" alt="Playwright" height="30" />
  <img src="https://cdn.simpleicons.org/vitest" alt="Vitest" height="30" />
  <img src="https://cdn.simpleicons.org/nodedotjs" alt="Node.js" height="30" />
</p>

## What Is Implemented

### Certification and Quiz System

- Certification hub with dedicated tracks for:
  - AWS
  - Azure
  - Salesforce Agentforce
  - MongoDB
  - PCAP Python
  - Oracle
- Practice and exam mode entry points per certification.
- Universal quiz runtime for immersive quiz sessions.
- AI quiz assistant (Bob) integrated across key quiz and home surfaces.

### AI Interview Simulator

- Interview setup and session flow for behavioral and technical interviews.
- Voice pipeline using browser speech APIs and Azure Speech fallback/token flow.
- In-session coding panel and interview analytics summary.
- Interview session history with persisted session stats.

### Competitive and Hands-On Practice

- Arena mode with matchmaking flow, battle loop, and results.
- Project Mode for multi-file challenge solving.
- Daily Challenge with language selection and code execution hooks.
- System Design canvas with node/connection editing, templates, and exports.

### Resume and Career Toolkit

- Resume Roaster with ATS-oriented feedback and actionable suggestions.
- ATS Score Optimizer view integrated into the career path workflow.
- Resume Builder with PDF generation endpoint at `/api/resume/generate`.
- Career Pathfinder analysis with tracker integration.

### Career Ops and Automation

- Career tracking actions and analytics utilities.
- Cron endpoints for:
  - scan
  - liveness
  - cadence recomputation
- Data contract documented in [docs/CAREER_OPS_DATA_CONTRACT.md](docs/CAREER_OPS_DATA_CONTRACT.md).

## Current Route Map

The app uses Next.js route groups (`(main)`, `(immersive)`, `(admin)`).
The group names do not appear in URLs.

| Area | Routes |
| --- | --- |
| Home and Core | `/`, `/dashboard`, `/settings`, `/about`, `/privacy`, `/terms` |
| Certification | `/certification`, `/aws-quiz/mode`, `/azure-quiz/mode`, `/salesforce-quiz/mode`, `/mongodb-quiz/mode`, `/pcap-quiz/mode`, `/oracle-quiz/mode`, plus immersive quiz runtime routes |
| Interview | `/demo`, `/demo/session`, `/demo/history` |
| Arena and Challenges | `/arena`, `/daily-challenge`, `/project-mode`, `/upload`, `/system-design` |
| Resume and Career | `/resume-roaster`, `/resume-builder`, `/career-path`, `/career-path/ats-score` |
| Admin | `/admin`, `/admin/leaderboard` |
| Utility/Internal | `/migrate`, `/api/health`, `/api/chat`, `/api/resume/generate`, `/api/cron/*` |

## Architecture

### Frontend and Routing

- Next.js 14 App Router with grouped layouts:
  - `app/(main)` for standard site experiences
  - `app/(immersive)` for full-screen modules
  - `app/(admin)` for admin console screens
- TypeScript + React 18 + Tailwind CSS + Framer Motion.

### Backend Surface

- Server actions in `app/actions/` for domain workflows:
  auth, quiz, interview, arena, dashboard, resume, career ops, project analysis, and more.
- API routes in `app/api/` for chat streaming, cron jobs, health checks,
  PDF generation, and blocked/rate-limited responses.

### AI Providers

- Provider strategy is implemented under `lib/ai/providers/`.
- Current Bob gateway behavior in `lib/ai/chat-gateway.ts`:
  - primary stream: Groq (`llama-3.3-70b-versatile`)
  - fallback stream: Gemini (`gemini-2.0-flash`)
- OpenAI provider implementation exists and can be used where configured.

### Data and Infra

- Supabase for auth and persistence.
- Upstash Redis for production API rate limiting and related cache patterns.
- Azure services for speech, document intelligence, and blob storage integrations.

For a package-level inventory, see [TECH_STACK.md](TECH_STACK.md).

## Getting Started

### Prerequisites

- Node.js 18+
- npm 9+
- A Supabase project for authenticated and persistent flows

### Install and Run

```bash
git clone https://github.com/2300030811/mockmate.git
cd mockmate
npm install
cp .env.example .env.local
npm run dev
```

PowerShell equivalent for env bootstrap:

```powershell
Copy-Item .env.example .env.local
```

Open http://localhost:3000

## Environment Variables

Use [.env.example](.env.example) as the source template.

### Commonly Needed for Local Development

- `NEXT_PUBLIC_APP_URL`
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`
- `SUPABASE_SERVICE_ROLE_KEY`
- At least one AI key:
  - `GOOGLE_API_KEY`
  - `GROQ_API_KEY`

### Feature-Specific Variables

- Rate limiting and cache:
  - `UPSTASH_REDIS_REST_URL`
  - `UPSTASH_REDIS_REST_TOKEN`
- Azure integrations:
  - `AZURE_SPEECH_KEY`
  - `AZURE_SPEECH_REGION`
  - `AZURE_DOCUMENT_INTELLIGENCE_ENDPOINT`
  - `AZURE_DOCUMENT_INTELLIGENCE_KEY`
  - `AZURE_STORAGE_CONNECTION_STRING`
- Resume/email/execution extras:
  - `RESEND_API_KEY`
  - `FEEDBACK_EMAIL`
  - `JUDGE0_API_KEY`
  - `RESUME_PDF_TIMEOUT_MS`
- Career Ops cron security:
  - `CRON_SCAN_SECRET`
  - `CRON_LIVENESS_SECRET`
  - `CRON_CAREER_OPS_SECRET`

The app is intentionally tolerant of partially configured environments, but
unconfigured features degrade or disable as expected.

## Scripts

| Script | Purpose |
| --- | --- |
| `npm run dev` | Start Next.js dev server |
| `npm run build` | Production build |
| `npm run start` | Run production server |
| `npm run lint` | ESLint checks |
| `npm run lint:fix` | Auto-fix lint issues where possible |
| `npm run type-check` | TypeScript `--noEmit` check |
| `npm run test` | Vitest in default mode |
| `npm run test:run` | Non-watch test run |
| `npm run test:watch` | Watch mode tests |
| `npm run test:coverage` | Coverage report (V8) |
| `npm run verify:career-ops` | Validate Career Ops env/files/contracts wiring |
| `npm run doctor:career-ops` | Diagnose Career Ops setup and test coverage expectations |

Coverage thresholds are configured in [vitest.config.mts](vitest.config.mts):

- lines: 70
- functions: 70
- statements: 70
- branches: 55

## Career Ops Runbook

### Canonical Contract

- Read and keep aligned with:
  [docs/CAREER_OPS_DATA_CONTRACT.md](docs/CAREER_OPS_DATA_CONTRACT.md)

### Verification Before Merge

```bash
npm run verify:career-ops
npm run doctor:career-ops
```

### Cron Endpoints

- `/api/cron/scan`
- `/api/cron/liveness`
- `/api/cron/cadence`

Auth supports either:

- `Authorization: Bearer <secret>`
- `x-cron-secret: <secret>`

Required migration files:

- `lib/db/migrations/add_career_ops_tracking.sql`
- `lib/db/migrations/add_career_ops_pattern_dimensions.sql`

## Security and Reliability

- Middleware updates Supabase session and applies production API rate limiting.
- Security headers are configured in `next.config.js` (CSP, HSTS, X-Frame-Options,
  X-Content-Type-Options, Referrer-Policy, Permissions-Policy).
- Health check endpoint available at `/api/health`.
- Runtime input validation uses Zod in key API and action surfaces.

## Project Structure

```text
mockmate/
|- app/
|  |- (main)/
|  |- (immersive)/
|  |- (admin)/
|  |- actions/
|  \- api/
|- components/
|- lib/
|  |- ai/
|  |- career-ops/
|  |- services/
|  \- db/
|- scripts/
|- docs/
|- templates/
|- types/
\- utils/
```

## Contributing

Contributions are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Keep changes focused and test-backed.
4. Run `npm run lint`, `npm run type-check`, and `npm run test:run`.
5. Open a PR with a clear summary and screenshots/logs when relevant.

## Team

| Name | Role | Links |
| --- | --- | --- |
| Bhima Mahesh Sai | Full Stack Developer | [GitHub](https://github.com/2300030811), [LinkedIn](https://www.linkedin.com/in/mahesh-sai-bhima-038243286) |
| Kondaveti Tejaswanth | Full Stack Developer | [GitHub](https://github.com/ktejaswanth), [LinkedIn](https://www.linkedin.com/in/ktejaswanth/) |

## License

MIT. See [LICENSE](LICENSE).
