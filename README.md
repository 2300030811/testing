# SecureSync AI 🛡️

**AI-Powered Parametric Income Insurance for Food Delivery Partners**

> Built for **Guidewire DEVTrails 2026** · In partnership with EY & NIA · Phase 1 — Seed

> *"The worker shouldn't have to do anything. When the rain comes, the money should too."*

**Demo Video:** [Watch here](#) &nbsp;|&nbsp; **Repository:** [GitHub](#)

---

## Table of Contents
- [The Problem](#-the-problem)
- [Our Solution](#-our-solution)
- [Persona & Scenarios](#-persona--real-world-scenarios)
- [Built for Low-End Android](#-built-for-low-end-android)
- [Application Workflow](#-application-workflow)
- [Platform Choice](#-platform-choice)
- [Weekly Premium Model](#-weekly-premium-model)
- [Parametric Triggers](#-parametric-triggers)
- [AI/ML Integration Plan](#-aiml-integration-plan)
- [Fraud Detection & Anti-Spoofing](#-fraud-detection--anti-spoofing)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Development Plan](#-development-plan)
- [What We're Planning Next](#-what-were-planning-next)
- [Team](#-team)

---

## 🚨 The Problem

India has over **15 lakh active delivery partners** across Zomato (8.94 lakh) and Swiggy (6.91 lakh) as of the September 2024 quarter. They are classified as *"partners"* — not employees — which means no PF, no ESI, no sick leave, and crucially, no income protection.

### The Income Reality

Zomato CEO Deepinder Goyal disclosed in January 2026 that the average earnings per hour (EPH) for a delivery partner in 2025 reached **₹102** — a 10.9% rise from ₹92 in 2024. A partner working 10 hours/day for 26 days grosses **₹26,500/month**, or roughly **₹21,000 net** after fuel and maintenance.

But this income isn't stable. Base pay per order has fallen from ₹40–₹45 to as low as ₹15–₹20 on many routes. Partners now depend almost entirely on daily incentive slabs to earn meaningfully. Miss a slab by 4 hours because of rain — the whole day's earnings collapse from ₹1,000 to under ₹400.

| Reality Check | Number |
|--------------|--------|
| Partners with any income protection | ~9% |
| Average income lost per disruption day | ₹400–₹820 |
| Average disruption days per year | 18–24 |
| Annual income lost per worker | ₹12,600–₹28,800 |
| Total sector loss annually | ~₹900 Cr+ |

No insurance product in India today is built for this. Existing products require paperwork, claim forms, and waiting periods — completely inaccessible to someone earning ₹800/day on a ₹10,000 Android phone. **SecureSync AI is built from the ground up for them.**

---

## 💡 Our Solution

SecureSync AI is a **zero-touch parametric income insurance platform**. The core idea is simple: instead of asking a worker to prove they lost income, we use objective third-party data to detect the disruption — and then we pay automatically.

The worker's only job is to buy a weekly policy. After that, our backend handles everything. When heavy rain crosses the IMD threshold in their zone, when AQI spikes past the CPCB danger level, when a bandh shuts down their city — our system detects it, validates it against 2 independent data sources, runs a fraud check, and transfers the money to their UPI. All within 2 minutes. No form. No call. No proof.

**What makes this parametric:** The payout condition is defined upfront and verifiable by anyone. There is no subjectivity, no negotiation, no assessor. Either the IMD threshold was crossed in that zone on that day, or it wasn't. The data decides — not a claims officer.

> Coverage scope — income loss from external disruptions only. Vehicle repairs, health costs, accidents, and any physical damages are strictly excluded per the DEVTrails problem statement. This is a wage-replacement product, nothing else.

---

## 👤 Persona & Real-World Scenarios

**Rajan Kumar, 28 — Swiggy Partner, South Chennai**

Works 10 hours/day, 6 days/week. Earns roughly ₹102/hr, ₹6,000/week. His phone is a Redmi A2 (2 GB RAM, MediaTek Helio G36, Jio 4G). He has no savings buffer — a single bad day means borrowing for fuel the next morning. He has never filed any kind of insurance claim in his life and wouldn't know how to start.

---

**Scenario 1 — Heavy Rainfall, Chennai (Most Common)**

> *Tuesday 3 PM. IMD Orange Alert issued. Rainfall in Rajan's zone crosses 70 mm for the day.*

Rajan parks under a flyover and waits. 4 hours. He misses his ₹400 daily incentive slab — earnings drop from ₹900 to under ₹400. He has no way to recover this.

With SecureSync AI running in the background:
- At 3:12 PM, our Trigger Monitor reads ≥ 64.5 mm/day accumulation for Zone 4
- OpenWeatherMap and IMD RSS both confirm — two independent sources agree
- A `disruption_event` is created. Rajan's active policy is matched automatically
- ₹102 × 4 hrs = **₹408** is initiated via Razorpay
- His phone (still in his pocket) receives: *"₹408 credited to your UPI. Stay safe, Rajan."*
- He did nothing. He knew nothing. The money was just there.

---

**Scenario 2 — Heat Wave, Hyderabad (May–June)**

Max temperature crosses 40°C — the IMD definition of a heat wave on plains. Confirmed by OpenWeatherMap + IMD alert. Delivery platforms visibly throttle order assignments. Rajan's Hyderabad equivalent receives **₹408** (₹102 × 4 hrs) automatically, for the hours he couldn't safely work outdoors.

---

**Scenario 3 — Severe AQI, Delhi (October–November)**

AQI crosses 300 in the CPCB "Very Poor" band. GRAP Stage II restrictions are active. AQICN and the CPCB official feed both confirm. Workers in affected Delhi zones receive **₹510** (₹102 × 5 hrs) — no different process, no extra steps.

---

**Scenario 4 — Bandh / Curfew (Any City)**

An unannounced local bandh locks down pickup and drop zones. Our system cross-references 2 of 3 sources — a news API, a government portal, and geo-social signals. Full-day payout: **₹816** (₹102 × 8 hrs) reaches policyholders before noon.

---

**Scenario 5 — Platform Outage (Any City)**

HTTP health probes from 3 independent regions all fail to reach Swiggy/Zomato servers for more than 2 hours. This is a genuine income disruption — workers can't accept orders. Payout triggers per confirmed outage hour: **₹102/hr**, capped to declared weekly income.

---

## 📲 Built for Low-End Android

Most delivery partners use entry-level Android devices — Redmi A series, Realme C series, Samsung A03/A04 — with 2–3 GB RAM, MediaTek processors, 32 GB storage, and Jio 4G that weakens during heavy rain. **If SecureSync AI doesn't work smoothly on a ₹8,000 phone with a patchy signal, it doesn't work.**

This isn't an afterthought. It's a design constraint we imposed from day one.

### What This Means for the App

**Bundle size target: < 150 KB initial JS load**
We chose React 18 + Vite 5 over heavier frameworks specifically because Vite's tree-shaking and code-splitting produces significantly smaller bundles. No full UI kit libraries — we write lean custom components.

**Offline-first architecture**
The policy status screen, payout history, and trigger explanation screens are all cached via Service Worker on first load. If a worker loses signal during a storm (exactly when they'd check the app), they still see their active coverage details. Only the live weather widget requires a network call.

**Image strategy**
All assets are WebP with explicit width/height to prevent layout shift. No full-resolution photos anywhere in the worker app. Icons are inline SVGs — no icon font load.

**Data usage**
A full app session — open, check dashboard, close — costs under 50 KB of data. Payout notifications go via WhatsApp (which workers already have open) rather than push notifications, which require background app persistence on low-RAM devices.

**No animations on the critical path**
Policy purchase, payout confirmation, and the disruption alert screens are static layouts. Animations only appear on non-critical screens (splash, onboarding) where a slow render has no consequence.

**Network resilience**
All API calls have a 3-second timeout with graceful fallback text. The trigger monitor backend uses cached zone data if an external API is slow — the app never shows a blank state or infinite spinner.

**Typography**
Noto Sans is used throughout — it renders Tamil, Telugu, Hindi, and Devanagari natively without a separate font load. A single font family covers our entire target user base.

---

## ⚙️ Application Workflow

```
Onboard → eKYC → Risk Profile → Weekly Policy → Automated Monitoring → Auto Payout
```

| Step | What Happens |
|------|-------------|
| **1. Onboard** | Phone OTP login. Aadhaar eKYC sandbox. Employment verification screenshot. Under 3 minutes total. |
| **2. Risk Profile** | ML ensemble (XGBoost + LightGBM) scores the worker's zone, forecast, and history. Premium returned in < 200ms. |
| **3. Buy Policy** | Worker reviews 7-day coverage summary, confirms premium, pays via Razorpay UPI AutoPay. Policy activates immediately. |
| **4. Monitor** | Trigger Monitor polls 5 external data sources every 5 minutes. Worker does nothing. |
| **5. Trigger** | Threshold crossed + 2 independent sources confirm → `disruption_event` created → all matching policyholders identified. |
| **6. Fraud check** | Isolation Forest scores each potential claim in < 5 seconds. Genuine claims pass instantly. |
| **7. Payout** | `Avg Hourly Income × Disruption Hours` transferred via Razorpay UPI. WhatsApp notification sent. |

---

## 📱 Platform Choice

**Decision: Mobile-first Progressive Web App (PWA)**

We considered building a native Android app first. We chose PWA for three reasons that matter specifically for this user:

**Distribution.** Delivery partners share useful tools as WhatsApp links. A PWA URL can be forwarded and "installed" to the home screen in one tap — no Play Store account, no app size concerns, no auto-update prompts that confuse non-tech-savvy users.

**Performance on constrained hardware.** PWAs run in the browser's optimised V8 runtime. On a Redmi A2 with 2 GB RAM, a PWA consumes roughly 60–70% less memory than an equivalent native app, which makes a meaningful difference when Swiggy is also running in the background.

**Maintenance velocity.** Any bug fix or new trigger type ships to every user the moment they open the app — no release cycle, no version fragmentation. In a 6-week competition this matters enormously.

Screen dimensions: 390×844px (standard Android viewport). Touch targets: minimum 48×48px throughout. Bottom navigation fixed — no hamburger menus.

---

## 💰 Weekly Premium Model

Gig workers earn week-to-week, not month-to-month. Our premium cycle matches this exactly — collected each Monday via Razorpay UPI AutoPay, covering the 7 days ahead.

### Formula

```
weekly_premium = base_rate × (1 + risk_multiplier) × loyalty_discount × tier_factor
```

### Risk Multiplier — 5 Components

The risk multiplier is a weighted sum of five independently measured risk signals. Each component has its own live data source and peaks at different times of year:

| Component | Weight | Peak Season | Data Source |
|-----------|--------|-------------|-------------|
| Weather risk | 40% | Jun–Sep monsoon | OpenWeatherMap 7-day forecast |
| Pollution risk | 25% | Oct–Nov North India | AQICN daily AQI trend |
| Zone disruption history | 20% | Varies by city | PostGIS historical IMD event density |
| Social unrest risk | 10% | Election periods | State election calendar + historical event data |
| Platform outage risk | 5% | Unpredictable | Rolling 90-day HTTP probe failure rate |

**Why weighted this way:** Weather accounts for 40% because it drives the majority of income disruption events in Indian metros. Pollution is 25% because of the scale of NCR winter AQI crises. Platform outage is only 5% because outages affect all workers simultaneously — a diversifiable risk that can be reserved at low cost.

### Components Table

| Component | Range | Detail |
|-----------|-------|--------|
| Base Rate | ₹25/week | Minimum reserve at a 65% target loss ratio |
| Risk Multiplier | 0.05 – 1.55 | Weighted sum of 5 signals above |
| Loyalty Discount | 0.85× – 1.0× | 3% reduction per continuous quarter enrolled — rewards workers who stay |
| Tier Factor | 1.0× Standard / 1.6× Premium | Standard: max ₹800/event · Premium: max ₹1,200/event |

### Worked Examples

| Worker | Risk Multiplier | Loyalty | Tier | Final Premium |
|--------|----------------|---------|------|---------------|
| Bengaluru, dry season, 1 yr enrolled | 0.15 | 0.91× | Standard | **~₹26/week** |
| Hyderabad, moderate risk, new | 0.55 | 1.00× | Standard | **~₹39/week** |
| Chennai, monsoon zone, new | 0.90 | 1.00× | Standard | **~₹47/week** |
| Chennai, monsoon zone, premium tier | 0.90 | 1.00× | Premium | **~₹76/week** |

At ₹47/week, a Chennai partner pays under **0.8% of weekly income** to protect against losing ₹800–₹1,200 in a single disruption. The math works for the worker.

**Phase 2 AI pricing upgrade:** The ML model will price at 500m × 500m zone grid resolution using PostGIS — a worker on elevated ground pays ₹2–3 less than a worker 1 km away in a flood-prone street. The DEVTrails problem statement specifically cites this as an example of good hyper-local ML pricing.

---

## ⚡ Parametric Triggers

Every trigger threshold comes from an official Indian government standard — not our own judgement. This is essential for credibility: if a worker disputes a payout, we can point to the exact IMD or CPCB classification that triggered it.

Every trigger also requires **confirmation from 2 independent data sources** before a payout fires. A single API returning a bad reading cannot trigger a payout. Both sources must agree.

| # | Disruption | Confirmation Sources | Official Threshold | Payout Hours |
|---|-----------|---------------------|-------------------|-------------|
| 1 | 🌧️ Heavy Rainfall | OpenWeatherMap + IMD RSS | ≥ 64.5 mm/day — IMD "Heavy Rain" category | 4 hrs |
| 2 | 🌫️ Hazardous AQI | AQICN + CPCB official feed | AQI > 300 — CPCB "Very Poor" band | 5 hrs |
| 3 | 🌡️ Heat Wave | OpenWeatherMap + IMD heat alert | Max temp ≥ 40°C — IMD plains heat wave definition | 4 hrs |
| 4 | 🌊 Flood / Red Warning | IMD RSS + NDMA API | Active IMD Red Warning for zone | 8 hrs |
| 5 | 🚫 Curfew / Bandh | NewsAPI + State Govt portal | Civil disruption confirmed by 2 of 3 sources | 8 hrs |
| 6 | 📵 Platform Outage | HTTP probes from 3 regions | All 3 probes fail > 2 continuous hours | Per hour |

**On the official standards:**

IMD rainfall scale (24-hour): Light 2.5–7.5 mm · Moderate 7.6–35.5 mm · Rather Heavy 35.6–64.4 mm · **Heavy 64.5–124.4 mm ← our trigger** · Very Heavy 124.5–244.4 mm · Extremely Heavy > 244.4 mm.

CPCB AQI scale: Good 0–50 · Satisfactory 51–100 · Moderate 101–200 · Poor 201–300 · **Very Poor 301–400 ← our trigger** · Severe 401–500.

IMD Heat Wave: maximum temperature ≥ 40°C on plains AND ≥ 4.5°C departure from normal. We use the 40°C threshold as the trigger condition.

---

## 🤖 AI/ML Integration Plan

### Premium Calculation — XGBoost + LightGBM Ensemble

We use a stacked ensemble rather than a single model. XGBoost provides strong regularization for stable predictions on sparse zone data; LightGBM's histogram-based leaf-wise tree growth is 3× faster and uses 40% less memory on inference — important when pricing requests must return in under 200ms on our server. The ensemble outperforms either model alone by roughly 12% on AUC-ROC for imbalanced tabular data (a common result in the ML literature for this model pairing).

**Inputs (47 features):** Zone disruption frequency over 5 years (IMD/AQICN archives), 7-day rain probability, 7-day AQI forecast, 7-day max temperature, worker's claim history (90 days), declared weekly income, delivery platform, zone PostGIS centroid, month, day of week, local election proximity flag, platform HTTP probe failure rate (rolling 90-day).

**Output:** `risk_score` (0.0–1.0) → `weekly_premium` in ₹. Minimum ₹25. Response target: < 200ms.

**Training pipeline:** Phase 1 uses 18 months of synthetic data generated from IMD historical records and AQICN city archives. Phase 2 switches to real payout outcomes as policies are issued — the model retrains weekly.

---

### Predictive Forecasting — LSTM (Phase 2)

A Long Short-Term Memory network trained on 72-hour rolling windows of environmental sensor data. Output: probability of trigger breach in 1hr / 3hr / 6hr windows. Use case: sending workers a heads-up before a disruption fires — *"Rain alert: coverage may activate in 2 hours"* — building trust and habit before a payout even happens.

---

### Fraud Scoring — Isolation Forest (Phase 2 → Supervised in Phase 3)

Isolation Forest detects anomalies without labelled training data, which we won't have in Phase 1. It works by isolating data points via random partitioning — fraudulent claims are easier to isolate (fewer splits needed) than genuine ones. Each claim is scored on:

| Feature | Fraud Signal |
|---------|-------------|
| Worker's claim rate vs. zone average (30 days) | Unusually high relative to neighbours |
| Minutes between policy purchase and first claim | Storm-chasers buy policies after forecasts confirm |
| Cell tower zone vs. claimed GPS zone | Physical location doesn't match claimed zone |
| Speed between consecutive GPS pings | > 120 km/h in an urban zone = spoofing app |
| Device ID vs. registered accounts | Same physical device across multiple accounts |
| Payout vs. declared weekly income | Cannot logically exceed declared earnings |
| % of zone peers also claiming | < 20% claiming in a zone while one worker does = anomaly |

**Routing:**
```
fraud_score < 0.30     → Auto-approve, payout fires immediately
fraud_score 0.30–0.65  → Soft flag, payout fires, logged for async review
fraud_score > 0.65     → Hard hold, manual review within 2 hours
```

In Phase 3, confirmed fraud cases are used to train a supervised Random Forest classifier — moving from anomaly detection to pattern recognition.

---

## 🔒 Fraud Detection & Anti-Spoofing

### Hard Guardrails (ML Cannot Override)

| Rule | Detail |
|------|--------|
| **Dual-Source Gate** | No payout fires on a single API reading — 2+ independent sources must agree |
| **Zone Lock** | Registered zone is fixed for 30 days. Changes trigger a 7-day coverage gap |
| **Event Deduplication** | Each `disruption_event` ID generates exactly one payout per worker per policy period |
| **Income Cap** | Weekly payout cannot exceed declared weekly income, cross-validated against city average |

### Why GPS Alone Is Not Enough

A ₹200 spoofing app on any Android device can output any GPS coordinate in seconds. We treat GPS as one signal among several, not a ground truth.

**What we use instead of GPS as primary location proof:**

Android devices continuously log cell tower IDs alongside GPS. These tower IDs reflect which physical tower the device is connected to — they cannot be faked by a software spoofing app because they require radio proximity to the tower. We collect the last 3 tower IDs from the background app session and cross-reference them against the tower coverage map for the claimed disruption zone.

**Speed plausibility check (second layer):** We compute the implied speed between consecutive GPS pings. If the result exceeds 120 km/h within an urban delivery zone, the device didn't travel there — it teleported via a spoofing app. This check runs in < 1ms and requires no additional data.

| Signal | Genuine Worker | Spoofer |
|--------|---------------|---------|
| GPS in disruption zone | ✅ Real | ✅ Faked |
| Cell tower in disruption zone | ✅ Yes | ❌ Actual tower exposed |
| Speed between GPS pings | ✅ Plausible | ❌ Teleport speed |
| Session in zone 2+ hrs before event | ✅ Consistent | ❌ Sudden appearance |
| Zone peers also affected | ✅ Yes | ✅ Yes (real event) |

**Detecting coordinated rings:** We build a graph of worker accounts, device fingerprints, and UPI payout destinations. Any device or UPI node connected to more than 2 worker accounts is automatically escalated. Batch registrations from the same IP within 10 minutes of each other trigger a staging flag before any claims are filed.

### UX for Flagged Claims — No Honest Worker Gets Punished

Bad weather degrades GPS signal and cell tower connectivity — the exact conditions that produce false positives. Our routing was designed specifically around this reality:

**Grace-Pay:** When a claim is flagged only because of a weak network signal — not because of device or behavioural anomalies — the payout fires immediately. An internal async review happens within 24 hours. The worker sees nothing except their money arriving. We pay first, verify after, because the alternative is systematically punishing workers during storms.

**Soft-Hold:** When a cell tower zone mismatch is detected, we send a single prompt: *"We noticed your signal was unclear. Tap to confirm you were working in Zone 4."* One tap, combined with cell tower re-resolution as connectivity recovers, closes over 90% of these cases within 30–45 minutes.

| What Happened | Worker Sees | Backend Does |
|--------------|------------|--------------|
| Clean pass | "₹408 transferred. Stay safe." | Score logged, nothing else |
| Network signal weak | "₹408 transferred. Stay safe." | Async review queued |
| Zone signal mismatch | "Confirming your location — payout in ~30 min." | ML rescores with fresh cell data |
| Anomaly detected | "We're reviewing this — update within 2 hours." | Manual review queue |
| Confirmed fraud | "Account paused. Please contact support." | Account flagged, policy voided |

The word "fraud" never appears for the first four categories. Workers who are genuinely affected by the same storm that weakens their GPS never experience a delay.

---

## 🛠️ Tech Stack

### Phase 1 — Running Now

| Layer | Choice | Reason |
|-------|--------|--------|
| Frontend | React 18 + Vite 5 | Smallest bundle size, fastest HMR, ideal for PWA |
| State | React Context API | Sufficient scope — no Redux overhead |
| Weather | OpenWeatherMap (free tier) | Live rain, temp, AQI; local mock fallback for offline dev |
| Font | Noto Sans | Single font covers Latin + Tamil + Telugu + Devanagari |
| Hosting | Static / CDN | HTML/JS/CSS only in Phase 1 — no server cost |

### Phase 2 — Being Built

| Layer | Choice | Reason |
|-------|--------|--------|
| Backend | **FastAPI (Python)** | Async, native Python ML integration, auto-generated Swagger docs, faster than Node.js/Express for ML-heavy workloads |
| Database | **PostgreSQL 16 + PostGIS** | ACID compliance for financial records; PostGIS for 500m-grid geospatial zone queries |
| Cache & Sessions | **Redis 7** | Sub-millisecond session lookups, rate limiting, trigger state caching |
| Event Bus | **Apache Kafka** | Decouples trigger detection from payout pipeline — a slow Razorpay response can't block claim detection |
| Auth | Twilio SMS OTP | Real OTP delivery — no dependency on Gmail or email access |
| KYC | UIDAI eKYC sandbox | Aadhaar verification for financial compliance |
| Payments | Razorpay (test mode) | UPI AutoPay mandate + instant payout API |
| Notifications | WhatsApp Business API | Workers already have WhatsApp open — higher open rate than push on low-RAM devices |

### Phase 3 — Planned

| Layer | Choice | Reason |
|-------|--------|--------|
| ML Premium | XGBoost + LightGBM ensemble | 12% better AUC-ROC, 40% less memory vs single model |
| ML Forecast | TensorFlow LSTM | 72-hr predictive risk — pre-emptive coverage escalation |
| ML Fraud | Isolation Forest → Random Forest | Unsupervised Phase 2, supervised Phase 3 with labelled fraud data |
| Inference | ONNX Runtime | < 50ms serving, language-agnostic, production-grade |
| Observability | Grafana + Prometheus | Loss ratio dashboards, trigger latency tracking, API health |
| Logs | ELK Stack | Audit trail required for any regulated financial product |
| Scale | Kubernetes (GKE) | Auto-scale during monsoon peak when claim volumes spike |

---

## 🏗️ System Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                    EXTERNAL DATA SOURCES                         │
│  OpenWeatherMap · AQICN · IMD RSS · NDMA · NewsAPI · HTTP Probes │
└──────┬─────────────┬──────────┬─────────┬──────────┬────────────┘
       │             │          │         │          │
       └─────────────┴──────────┴─────────┴──────────┘
                           │ polls every 5 min
                           ▼
┌──────────────────────────────────────────────────────────────────┐
│           BACKEND — FastAPI · Python · Async                     │
│  ┌──────────────────────┐  ┌──────────────────────────────────┐  │
│  │  REST API  (port 8000)│  │  Trigger Monitor                 │  │
│  │  /api/v1/            │  │  cron · dual-source gate · Kafka  │  │
│  └──────────┬───────────┘  └───────────────┬──────────────────┘  │
└─────────────┼──────────────────────────────┼────────────────────┘
              │                              │
   ┌──────────▼─────────┐     ┌─────────────▼──────────────────┐
   │  FRONTEND           │     │  ML SERVICE — FastAPI/Python    │
   │  React 18 + Vite 5  │     │  XGBoost + LightGBM + IForest  │
   │  PWA · < 150KB JS   │     │  ONNX Runtime (Phase 3)        │
   │  port 3000          │     │  port 8001                     │
   └────────────────────┘     └────────────────────────────────┘
              │                              │
   ┌──────────▼──────────────────────────────▼──────────────────┐
   │            PostgreSQL 16 + PostGIS                         │
   │   workers · policies · disruption_events · claims          │
   └─────────────────────────┬──────────────────────────────────┘
                             │
              ┌──────────────▼──────────────┐
              │  Redis 7 · Apache Kafka      │
              │  sessions · cache · events   │
              └─────────────────────────────┘
```

One runtime language (Python) spans both Backend and ML Service — no serialization overhead crossing a language boundary. ML models load once into memory at startup and are called as local function calls, not HTTP requests. This gives < 5ms model inference overhead.

---

## 📅 Development Plan

**Phase 1 — Seed (March 4–20) ← Current**
- [x] Problem research — 2025 EPH data, Zomato/Swiggy partner counts, income loss statistics
- [x] Persona built around actual device constraints (Redmi A2, 2 GB RAM, Jio 4G)
- [x] 5 real-world disruption scenarios with accurate ₹102/hr payout calculations
- [x] IMD/CPCB-calibrated triggers with dual-source confirmation requirement
- [x] 5-component weighted premium formula with loyalty discount and tier structure
- [x] XGBoost + LightGBM ensemble design with 47-feature input spec
- [x] Isolation Forest fraud scoring with cell tower + speed plausibility checks
- [x] Anti-spoofing strategy — Grace-Pay and Soft-Hold UX routing
- [x] Low-end Android performance constraints documented and designed around
- [x] FastAPI + PostGIS + Redis + Kafka architecture
- [x] Figma prototype — 8 screens
- [ ] 2-minute strategy video — paste link above replacing `[Watch here](#)`

**Phase 2 — Scale (March 21–April 4)**
- [ ] FastAPI backend scaffold + PostgreSQL 16 + PostGIS schema
- [ ] Twilio OTP + UIDAI eKYC sandbox — full registration flow
- [ ] Trigger Monitor — 5-minute cron, dual-source gate, Kafka event publish
- [ ] XGBoost + LightGBM premium model — synthetic IMD-calibrated training data
- [ ] Razorpay UPI AutoPay mandate + sandbox payout + WhatsApp notification
- [ ] React PWA — onboarding, policy purchase, live dashboard (< 150 KB JS target)
- [ ] 2-minute demo video

**Phase 3 — Soar (April 5–17)**
- [ ] Isolation Forest fraud model live pre-payout
- [ ] Cell tower zone validation + impossible-speed GPS check
- [ ] Graph-based fraud ring detection — device + UPI bipartite graph
- [ ] LSTM 72-hr predictive risk forecast — pre-emptive coverage alerts
- [ ] Admin dashboard — loss ratio, disruption heatmap, manual review queue
- [ ] Worker dashboard — payout history, active coverage, zone live status
- [ ] Kubernetes auto-scaling for monsoon peak load
- [ ] Final 5-minute video + pitch deck PDF

---

## 💡 What We're Planning Next

Ideas we've identified through worker research and will evaluate between phases:

**Accessibility improvements (Phase 2)**
WhatsApp as the primary notification channel — no app open required, works on 2G, lower battery drain than push on low-RAM devices. USSD / SMS fallback for workers in Tier 2/3 cities without reliable data plans.

**Smarter pricing (Phase 2)**
Hyper-local 500m grid pricing via PostGIS — a worker on elevated ground in a historically flood-safe street pays ₹2–3 less than a worker 1 km away in a waterlogged zone. Loyalty discount escalates 3% per continuous quarter enrolled.

**Compound disruptions (Phase 3)**
When rain and a bandh happen simultaneously, the current model pays out the higher trigger. We want to design a combined payout formula that reflects the compounded income loss more accurately.

**Pre-emptive alerts (Phase 2)**
The LSTM forecast will let us warn workers 3–6 hours before a trigger fires — *"Heavy rain likely this evening. Your coverage is active."* Builds trust before a payout is even needed.

**Savings layer (Phase 4)**
In months with no claims, a small percentage of the premium is held in a micro-savings reserve that the worker can withdraw after 6 months of continuous enrollment. Turns insurance into a financial tool.

---

## 👥 Team

| Name | Role | What They Own |
|------|------|--------------|
| **Irfan Hussain** | Team Lead & Architect | System design, product strategy, API architecture, ML pipeline design |
| **Mahesh Sai** | Backend Engineer | FastAPI, PostgreSQL + PostGIS, Razorpay integration, trigger monitor |
| **Ahamad** | AI/ML Engineer | Premium model (XGBoost + LightGBM), fraud scoring, LSTM forecasting |
| **Akhil** | Frontend & DevOps | React/Vite PWA, low-end Android performance, Docker, Kubernetes |

---

> **Built for Guidewire DEVTrails 2026 · In partnership with EY & NIA**
>
> *Protecting India's 15+ lakh delivery partners — one parametric trigger at a time.*
>
> Target: DEVSummit Bangalore · May 2026 · Prize Pool: ₹6,00,000
