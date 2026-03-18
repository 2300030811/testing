# GigGuard
### AI-Powered Parametric Income Insurance for India's Gig Economy

<p align="center">
  <img src="https://img.shields.io/badge/Built%20for-Guidewire%20DEVTrails%202026-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Phase-1-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white" />
  <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
</p>

---

## 📖 Table of Contents

- [The Problem](#-the-problem)
- [Our Solution](#-our-solution)
- [How It Works](#-how-it-works)
- [Architecture](#-architecture)
- [Parametric Triggers](#-parametric-triggers)
- [AI-Powered Premium Model](#-ai-powered-premium-model)
- [Fraud Detection](#-fraud-detection)
- [Future Innovations](#-future-innovations)
- [Tech Stack](#-tech-stack)
- [Setup & Running](#-setup--running)
- [Documentation](#-documentation)

---

## 🚨 The Problem

India's gig economy is projected to surpass **23 million workers by 2030**. Food delivery partners, ride-share drivers, and other platform workers are classified as "partners" — not employees — meaning they receive **no traditional employment safety net**.

External disruptions like heavy rain, extreme heat, or hazardous air quality cause an estimated **20–30% monthly income loss** for these workers, yet existing insurance products are entirely misaligned with their daily financial realities. There is currently no practical, accessible solution for recovering even a single day's lost income.

**GigGuard is built to fill this void.**

---

## 💡 Our Solution

GigGuard provides an automated financial safety net by replacing the slow, paperwork-heavy claims process of traditional insurance with a **parametric engine** — a modern, data-driven approach where objective, verifiable data automatically triggers payouts.

**No forms. No waiting. No proof of loss required.**

> Instead of asking "did you lose income?", we ask "did the event happen?" — and the data answers for itself.

---

## ⚙️ How It Works

```
Worker buys policy → System monitors conditions → Threshold breached → Instant payout
```

| Step | Action | Detail |
|------|--------|--------|
| 1️⃣ | **Purchase** | Worker buys a flexible, low-cost weekly policy via our app. Price is determined in real-time by our AI model. |
| 2️⃣ | **Monitor** | Backend continuously polls OpenWeatherMap and AQICN for every covered delivery zone. |
| 3️⃣ | **Trigger** | When a threshold is crossed (e.g., rainfall > 15 mm/hr), a `disruption_event` is automatically created. |
| 4️⃣ | **Payout** | All policyholders in the affected zone receive instant compensation via Razorpay — zero manual steps required. |

**Compensation Formula:**
```
Payout = Average Hourly Income × Disruption Hours
```

---

## 🏗️ Architecture

GigGuard is built on a **scalable microservices architecture**, containerized with Docker for consistency across all environments. The four core services maintain a clear separation of concerns, enabling independent scaling and deployment.

![System Flow](docs/assets/system_flow.png)

| Service | Technology | Role |
|---------|------------|------|
| **Frontend** | Next.js 14, TypeScript | Worker onboarding, policy management, and claims dashboard |
| **Backend** | Node.js, Express, TS | Core API, business logic, DB management, and the trigger monitor cron job |
| **ML Service** | Python, Flask, Scikit-learn | Premium calculation and real-time fraud detection models |
| **Database** | PostgreSQL | Single source of truth for workers, policies, events, and claims |

> 📐 For the full database schema and API design, see the [Architecture Document](docs/architecture.md) and [ER Model](docs/GigGuard_ER_Model.pdf).

---

## ⚡ Parametric Triggers

Automated, objective thresholds that eliminate ambiguity and paperwork — a game-changer for workers who cannot afford to wait weeks for a manual review.

| Trigger | Data Source | Threshold | Disruption Hours |
|---------|-------------|-----------|-----------------|
| 🌧️ Heavy Rainfall | OpenWeatherMap API | > 15 mm/hr | 4 hours |
| 🌫️ Severe AQI | AQICN API | > 300 (PM2.5) | 5 hours |
| 🌡️ Extreme Heat | OpenWeatherMap API | > 44°C (Feels Like) | 4 hours |
| 🌊 Flood / Red Alert | IMD Mock RSS | Alert Active for Zone | 8 hours (Full Day) |
| 🚫 Curfew / Strike | Mock Webhook | Event Active for Zone | 8 hours (Full Day) |

> 📋 For detailed threshold justifications, fraud guard mechanisms, and API parsing logic, see the [Trigger Definitions Document](docs/trigger-definitions.md).

---

## 🤖 AI-Powered Premium Model

Pricing is **dynamic, not fixed**. A machine learning model calculates each worker's weekly premium in real-time, so workers in lower-risk areas pay less, and prices adjust with current forecasts.

**Formula:**
```
weekly_premium = base_rate × zone_multiplier × weather_multiplier × history_multiplier
```

| Component | Description |
|-----------|-------------|
| **Base Rate (₹35)** | Fixed cost covering basic operations |
| **Zone Multiplier** | AI-driven, reflects long-term historical risk of the worker's specific geographic zone |
| **Weather Multiplier** | Short-term adjustment based on the 7-day weather and air quality forecast |
| **History Multiplier** | Personal discount or surcharge based on individual claims history — rewards consistent, safe behavior |

**Example:** A Bengaluru delivery partner in a medium-risk zone with no prior claims and a fair forecast might pay **~₹80–100/week** to cover ₹5,000 in weekly earnings.

> 📊 For the complete formula breakdown and business viability analysis, see the [Premium Model Document](docs/premium-model.md).

---

## 🔒 Fraud Detection

To protect the platform and keep premiums sustainable, an **Isolation Forest** anomaly detection model analyzes every claim in real-time.

**How it works:**
- Assigns a fraud score to each claim based on features like claim frequency relative to the zone average, geolocation consistency, and time-of-event correlation
- **High-risk claims** are automatically flagged for a quick manual review
- **Low-risk, legitimate claims** are processed and paid out instantly

This approach keeps the claims pipeline fast and honest — without penalizing legitimate workers.

---

## 🚀 Future Innovations

A strategic roadmap of advanced features drawn from the world's leading technology companies.

| Innovation | Inspired By | Description |
|------------|-------------|-------------|
| **H3 Geospatial Indexing** | Uber | Replaces text-based zones with Uber's hexagonal grid for hyper-precise geographic accuracy, preventing payouts for unaffected workers |
| **Contextual Bandits** | Netflix | Personalizes policy recommendations using multi-armed bandit algorithms to show the right product to the right user |
| **Reinforcement Learning Premiums** | Uber / DeepMind | A self-tuning premium engine that learns optimal pricing to maximize purchase rates while maintaining a sustainable loss ratio |
| **Graph Neural Network Fraud** | Stripe Radar | Builds a relationship graph of users, claims, and payouts to detect coordinated fraud rings invisible to traditional models |
| **Causal Inference Validation** | Netflix / Spotify | Determines if a worker would have been offline regardless, ensuring we only pay for income loss *caused* by the disruption |
| **Smart Contract Execution** | AXA Fizzy | Encodes policy terms on a public blockchain (Polygon) to create tamper-proof, mathematically guaranteed insurance contracts |

> 📄 For technical details, schema changes, and timelines for each innovation, see the [Innovation Plan](docs/GigGuard_Innovation_Plan.pdf).

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Frontend** | Next.js 14, TypeScript | Worker onboarding, policy management, and claims history |
| **Backend** | Node.js, Express, TypeScript | Core business logic, API gateway, DB management, trigger polling |
| **Machine Learning** | Python, Flask, Scikit-learn | Premium calculation and fraud detection |
| **Database** | PostgreSQL | All persistent data — workers, policies, events, claims |
| **Payments** | Razorpay (Sandbox) | Automated payout execution |
| **Deployment** | Docker, Docker Compose | Containerized orchestration for all services |
| **External APIs** | OpenWeatherMap, AQICN, IMD RSS | Real-time disruption data sources |

---

## 🖥️ Setup & Running

### Prerequisites

- Node.js v18+
- Python v3.9+
- Docker and Docker Compose
- `pnpm` (or `npm`/`yarn`)

### Quickstart

**1. Clone the repository**
```bash
git clone https://github.com/your-repo/gigguard.git
cd gigguard
```

**2. Configure environment variables**
```bash
cp .env.example .env
# Fill in your API keys: OpenWeatherMap, AQICN, Razorpay Sandbox
```

**3. Install dependencies**
```bash
# Backend
pnpm install --prefix backend

# Frontend
pnpm install --prefix frontend

# ML Service
pip install -r ml-service/requirements.txt
```

**4. Run the full stack**
```bash
docker-compose up --build
```

### Service URLs

| Service | URL |
|---------|-----|
| Frontend App | http://localhost:3000 |
| Backend API | http://localhost:4000 |
| ML Service | http://localhost:5001 |

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [Architecture Deep Dive](docs/architecture.md) | Full system design, DB schema, and API specs |
| [Premium Model Details](docs/premium-model.md) | ML formula, risk factors, and viability analysis |
| [Trigger Definitions](docs/trigger-definitions.md) | Threshold justifications and fraud guard mechanisms |
| [Innovation Plan](docs/GigGuard_Innovation_Plan.pdf) | Roadmap with technical specs and timelines |
| [ER Model](docs/GigGuard_ER_Model.pdf) | Full database entity-relationship diagram |

---

<p align="center">
  <sub>Built with ❤️ for India's 23 million gig workers · Guidewire DEVTrails 2026</sub>
</p>
