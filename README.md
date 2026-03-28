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
- [Business Viability](#-business-viability)
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

**The disruption calendar never stops.** Chennai and Mumbai average 45+ heavy rain days per year. Delhi logs 30–40 zero-visibility fog mornings every winter. Every metro crosses AQI 300 at some point. None of this is covered by any existing product.

No insurance product in India today is built for this. Existing products require paperwork, claim forms, and waiting periods — completely inaccessible to someone earning ₹800/day on a ₹10,000 Android phone. **SecureSync AI is built from the ground up for them.**

---

## 💡 Our Solution

SecureSync AI is a **zero-touch parametric income insurance platform**. Instead of asking a worker to prove they lost income, we use objective third-party data to detect the disruption — and then we pay automatically.

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

Rajan parks under a flyover and waits 4 hours. He misses his ₹400 daily incentive slab — earnings drop from ₹900 to under ₹400. He has no way to recover this.

With SecureSync AI running in the background:
- At 3:12 PM, our Trigger Monitor reads ≥ 64.5 mm/day for Zone 4
- OpenWeatherMap and IMD RSS both confirm — two independent sources agree
- A `disruption_event` is created. Rajan's active policy is matched automatically
- ₹102 × 4 hrs = **₹408** initiated via Razorpay
- His phone receives: *"₹408 credited to your UPI. Stay safe, Rajan."*
- He did nothing. He knew nothing. The money was just there.

---

**Scenario 2 — Heat Wave, Hyderabad (May–June)**

Max temperature crosses 40°C — the IMD definition of a heat wave on plains. Confirmed by OpenWeatherMap + IMD alert. Delivery platforms throttle order assignments. Rajan's Hyderabad equivalent receives **₹408** (₹102 × 4 hrs) automatically.

---

**Scenario 3 — Severe AQI, Delhi (October–November)**

AQI crosses 300 — CPCB "Very Poor" band. GRAP Stage II active. AQICN and CPCB feed both confirm. Workers receive **₹510** (₹102 × 5 hrs). No different process, no extra steps.

---

**Scenario 4 — Dense Fog, Delhi / North India (December–January)**

> *6 AM, Delhi. Visibility has dropped to 40 metres. A two-wheeler can't safely leave the driveway.*

This is a disruption type most platforms ignore entirely — but Delhi and the Indo-Gangetic plains log 30–40 zero-visibility mornings every December and January. OpenWeatherMap's visibility field reads < 200m. Our Trigger Monitor catches it, confirms with the IMD fog advisory feed, and fires a 4-hour payout: **₹408** — before the worker would have even started his shift. This single trigger opens the entire North India winter market, a massive segment no competitor covers.

---

**Scenario 5 — Severe Traffic Gridlock (Any Metro)**

An accident or major event blocks arterial roads through a delivery zone during peak hours. Workers can't reach pickup points. TomTom Traffic API reports average zone speed below 8 km/hr for 60+ minutes. Our system cross-validates the drop in delivery activity and fires a **proportional payout** — calculated on the actual hours lost, not a flat estimate. Workers are compensated for the share of income they genuinely lost.

---

**Scenario 6 — Bandh / Curfew (Any City)**

An unannounced bandh locks down pickup and drop zones. System cross-references 2 of 3 sources — NewsAPI, state government portal, and geo-social signals. Full-day payout: **₹816** (₹102 × 8 hrs) reaches policyholders before noon.

---

**Scenario 7 — Platform Outage (Any City)**

HTTP probes from 3 independent regions all fail to reach Swiggy/Zomato servers for > 2 continuous hours. Workers can't accept orders. Payout fires per confirmed outage hour: **₹102/hr**, capped to declared weekly income.

---

## 📲 Built for Low-End Android

Most delivery partners use entry-level devices — Redmi A series, Realme C series, Samsung A03/A04 — with 2–3 GB RAM, MediaTek processors, 32 GB storage, and Jio 4G that weakens in heavy rain. **If SecureSync AI doesn't work smoothly on a ₹8,000 phone with a patchy signal, it doesn't work.**

This isn't an afterthought. It's a design constraint we imposed from day one.

### What This Means

**Bundle size target: < 150 KB initial JS load**
React 18 + Vite 5 produces the leanest possible bundles via tree-shaking and code-splitting. No full UI kit imports — every component is handwritten.

**Adaptive GPS sampling**
Stationary or offline: checked every 30 minutes. Active and moving: every 2 minutes. This keeps GPS battery consumption **under 3% per day** — versus the 8–12% typical of continuous-tracking apps. Workers running Swiggy simultaneously on the same device won't notice SecureSync's battery footprint.

**Data budget: < 40 MB/month**
A full app session — open, check dashboard, close — costs under 50 KB of data. Payout notifications go via WhatsApp (already open, works on 2G, zero extra cost) rather than push notifications that require background app persistence on low-RAM devices. Total monthly data stays under 40 MB.

**Offline-first architecture**
Policy status, payout history, and trigger explanation screens are cached via Service Worker on first load. If a worker loses signal during a storm — exactly when they'd check the app — they still see their active coverage. Only the live weather widget needs a network call.

**No animations on the critical path**
Policy purchase, payout confirmation, and the disruption alert screens are static layouts. Animations only appear on splash and onboarding — where a slow render has no consequence.

**Network resilience**
All API calls carry a 3-second timeout with graceful fallback text. The trigger monitor serves cached zone data if an external API is slow. The app never shows a blank screen or an infinite spinner.

**Typography**
Noto Sans renders Tamil, Telugu, Hindi, and Devanagari from a single font file — our entire user base covered without an additional load.

---

## ⚙️ Application Workflow

```
Onboard → Partner Verification → Risk Profile → Weekly Policy → Automated Monitoring → Auto Payout
```

| Step | What Happens |
|------|-------------|
| **1. Onboard** | Phone OTP login. Worker enters their Swiggy or Zomato Partner ID — we verify it directly against the platform's partner database. This confirms they are an active gig worker, extracts their registered delivery zone, and seeds their platform tenure score into the fraud model. Under 2 minutes. |
| **2. Risk Profile** | XGBoost + LightGBM ensemble scores zone, forecast, and history. Premium returned in < 200ms. Worker sees a plain-language SHAP breakdown of why they pay what they pay. |
| **3. Buy Policy** | Worker reviews 7-day coverage summary, pays via Razorpay UPI AutoPay. Policy activates immediately. |
| **4. Monitor** | Trigger Monitor polls 6 external data sources every 5 minutes. Worker does nothing. |
| **5. Trigger** | Threshold crossed + 2 independent sources confirm → `disruption_event` → policyholders identified. |
| **6. Fraud check** | Multi-layer engine including delivery activity cross-validation. Genuine claims pass in < 5 seconds. |
| **7. Payout** | `Avg Hourly Income × Disruption Hours` transferred via Razorpay. WhatsApp notification sent. |

---

## 📱 Platform Choice

**Decision: Mobile-first Progressive Web App (PWA)**

**Distribution.** Partners share useful tools via WhatsApp links. A PWA installs to the home screen in one tap — no Play Store account, no app size concerns, no update prompts that confuse non-tech-savvy users.

**Performance.** On a Redmi A2 with 2 GB RAM, a PWA consumes 60–70% less memory than a native app — a real difference when Swiggy is running simultaneously.

**Velocity.** Bug fixes and new trigger types ship the moment a worker opens the app. No release cycle. No version fragmentation. Critical in a 6-week competition.

Screen: 390×844px. Touch targets: 48×48px minimum. Fixed bottom navigation — no hamburger menus.

---

## 💰 Weekly Premium Model

Gig workers earn week-to-week. Our premium cycle matches exactly — collected each Monday via Razorpay UPI AutoPay, covering the 7 days ahead.

### Formula

```
weekly_premium = base_rate × (1 + risk_multiplier) × loyalty_discount × tier_factor
```

### Why Partner ID, Not Aadhaar eKYC

Most platforms default to Aadhaar eKYC because it's the obvious identity layer in India. We deliberately chose not to, for three reasons:

**It proves the right thing.** Aadhaar confirms identity. A Swiggy or Zomato Partner ID confirms the person is an *active gig worker on that platform* — which is precisely what we need. We're not an identity product. We're an income protection product. Verifying employment is more relevant than verifying existence.

**It unlocks richer data.** A Partner ID lookup returns the worker's registered delivery zone, account creation date, and active/inactive status — data we need anyway for the premium model and fraud layer. Aadhaar gives us none of that. One API call does the job of three.

**It's practically achievable.** UIDAI eKYC access for a financial product requires regulatory sandbox approvals that take months. Swiggy and Zomato already expose partner verification endpoints for fleet management tools. In Phase 2 we mock this with a static partner database. In Phase 3 we integrate with real platform APIs or simulate the OAuth flow. The dependency chain is shorter and the data quality is higher.

| Component | Weight | Peak Season | Data Source |
|-----------|--------|-------------|-------------|
| Weather risk | 40% | Jun–Sep monsoon | OpenWeatherMap 7-day forecast |
| Pollution risk | 25% | Oct–Nov North India | AQICN daily AQI trend |
| Zone disruption history | 20% | Varies by city | PostGIS historical IMD event density |
| Social unrest risk | 10% | Election periods | State election calendar + historical events |
| Platform outage risk | 5% | Unpredictable | Rolling 90-day HTTP probe failure rate |

### Components Table

| Component | Range | Detail |
|-----------|-------|--------|
| Base Rate | ₹25/week | Minimum reserve at 65% target loss ratio |
| Risk Multiplier | 0.05 – 1.55 | Weighted sum of 5 signals |
| Loyalty Discount | 0.85× – 1.0× | 3% off per continuous quarter enrolled |
| Tier Factor | 1.0× or 1.6× | Standard: max ₹800/event · Premium: max ₹1,200/event |

### Worked Examples

| Worker | Risk Multiplier | Loyalty | Tier | Final Premium |
|--------|----------------|---------|------|---------------|
| Bengaluru, dry season, 1 yr enrolled | 0.15 | 0.91× | Standard | **~₹26/week** |
| Hyderabad, moderate risk, new | 0.55 | 1.00× | Standard | **~₹39/week** |
| Chennai, monsoon zone, new | 0.90 | 1.00× | Standard | **~₹47/week** |
| Chennai, monsoon zone, premium tier | 0.90 | 1.00× | Premium | **~₹76/week** |

At ₹47/week, a Chennai partner pays **under 0.8% of weekly income** to protect against an ₹800–₹1,200 single-disruption loss.

### Premium Explainability — Workers Understand What They Pay

Using SHAP values from the XGBoost model, every worker sees a plain-language breakdown at policy purchase:

> *"Your weekly premium is ₹47. You pay ₹3 extra because your zone has a high rainfall forecast this week. You save ₹2 because your claim history is clean."*

This transparency reduces abandonment at the payment screen. Workers who understand their pricing renew consistently — it's trust built before a payout ever needs to fire.

**Phase 2 AI upgrade:** 500m × 500m zone grid pricing via PostGIS — a worker on elevated ground pays ₹2–3 less than a worker 1 km away in a flood-prone street.

---

## ⚡ Parametric Triggers

Every threshold comes from an official Indian government standard. Every trigger requires **2 independent data sources to agree** before a payout fires. A single API with a bad reading cannot trigger a payout alone.

| # | Disruption | Sources Required | Threshold | Payout |
|---|-----------|-----------------|-----------|--------|
| 1 | 🌧️ Heavy Rainfall | OpenWeatherMap + IMD RSS | ≥ 64.5 mm/day — IMD "Heavy Rain" | 4 hrs × hourly rate |
| 2 | 🌫️ Hazardous AQI | AQICN + CPCB official feed | AQI > 300 — CPCB "Very Poor" | 5 hrs × hourly rate |
| 3 | 🌡️ Heat Wave | OpenWeatherMap + IMD heat alert | Max temp ≥ 40°C — IMD plains definition | 4 hrs × hourly rate |
| 4 | 🌊 Flood / Red Warning | IMD RSS + NDMA API | Active IMD Red Warning for zone | 8 hrs × hourly rate |
| 5 | 🌁 Dense Fog / Zero Visibility | OpenWeatherMap visibility + IMD fog advisory | Visibility < 200m for ≥ 2 hrs | 4 hrs × hourly rate |
| 6 | 🚗 Severe Traffic Gridlock | TomTom Traffic API + delivery activity drop | Zone avg speed < 8 km/hr for 60+ min (peak hours) | Proportional to hours lost |
| 7 | 🚫 Curfew / Bandh | NewsAPI + State Govt portal (2 of 3) | Civil disruption confirmed in zone | 8 hrs × hourly rate |
| 8 | 📵 Platform Outage | HTTP probes from 3 regions | All 3 fail > 2 continuous hours | Per confirmed outage hour |

**Why 8 triggers win:** Most competing platforms stop at 3–5 triggers. We cover the full disruption calendar. Dense fog alone opens the entire North India winter market — Delhi, UP, Punjab — which no other platform addresses specifically. Traffic gridlock adds a new category of income disruption that has nothing to do with weather.

**Proportional payout for traffic:** Unlike complete work stoppages, severe traffic causes partial income loss. We calculate `hours_of_disruption × (1 - activity_ratio) × hourly_rate` — workers are compensated for what they actually lost, not a flat estimate.

**Official standards:**
- IMD (24hr): Rather Heavy 35.6–64.4 mm · **Heavy ≥ 64.5 mm ← trigger** · Very Heavy ≥ 124.5 mm
- CPCB: Poor 201–300 · **Very Poor 301–400 ← trigger** · Severe 401–500
- IMD Heat Wave: max temp ≥ 40°C AND ≥ 4.5°C departure from climatological normal

---

## 🤖 AI/ML Integration Plan

### Premium Calculation — XGBoost + LightGBM Ensemble

We use a stacked ensemble. XGBoost contributes strong regularization for stable predictions on sparse zone data; LightGBM's histogram-based leaf-wise growth is 3× faster and uses 40% less memory — important for < 200ms response targets. The ensemble outperforms either model alone by roughly 12% on AUC-ROC for imbalanced tabular data.

**Inputs (47 features):** Zone disruption frequency over 5 years (IMD/AQICN archives), 7-day rain/AQI/temperature/visibility forecast, traffic congestion history, worker's claim history (90 days), declared weekly income, delivery platform, zone PostGIS centroid, month, election proximity flag, platform probe failure rate.

**Output:** `risk_score` (0.0–1.0) → `weekly_premium` in ₹, minimum ₹25, in < 200ms.

**SHAP explainability:** After every premium calculation, SHAP values generate a plain-language one-liner that tells the worker exactly why their number is what it is. No black box pricing.

**Training:** 18 months synthetic IMD-calibrated data. Retrains weekly on real payout outcomes.

---

### Predictive Forecasting — LSTM (Phase 2)

Long Short-Term Memory network on 72-hour rolling environmental data. Output: disruption breach probability at 1hr / 3hr / 6hr horizons. Use: warn workers before a trigger fires — *"Heavy rain likely in your zone in 3 hours. Your coverage is watching."* Builds trust before money ever changes hands.

---

### Fraud Scoring — Multi-Layer (Phase 2 rules → Phase 3 ML)

```
fraud_score < 0.30     → Auto-approve, payout fires immediately
fraud_score 0.30–0.65  → Soft flag, payout fires, async review logged
fraud_score > 0.65     → Hard hold, manual review within 2 hours
```

Phase 2: rule-based scoring with delivery activity cross-validation. Phase 3: Isolation Forest → supervised Random Forest as confirmed fraud cases accumulate.

---

## 🔒 Fraud Detection & Anti-Spoofing

### Hard Guardrails — Cannot Be Overridden by the ML Model

| Rule | Detail |
|------|--------|
| **Dual-Source Gate** | No payout fires on a single API reading — 2+ independent sources must confirm the disruption |
| **Zone Lock** | Registered zone fixed for 30 days; changes trigger a 7-day coverage gap |
| **Event Deduplication** | One payout per worker per `disruption_event` regardless of event duration |
| **Income Cap** | Weekly payout cannot exceed declared weekly income, validated against city average |
| **Coordinated Surge Detection** | More than 40 claims arriving within an 8-minute window for a single event triggers an automatic hold. Organic claims trickle in over hours. Fraud rings file in minutes. |

### Layer 1 — Delivery Activity Cross-Validation

The most powerful fraud signal is the one a bad actor cannot touch: **what the delivery platform's own backend says about whether the worker was actually offline.**

For workers who have connected their Swiggy or Zomato account, when a claim is triggered, we cross-check delivery activity status during the disruption window. If the platform's servers show active order completions during the claimed disruption, the claim is immediately flagged — before GPS checks, before ML models. This is data from the platform's infrastructure, not the worker's device. It cannot be spoofed by a location app.

GPS data can be manipulated by a ₹200 app. Delivery platform activity data cannot be manipulated from a worker's device. The two sources are independent — which is precisely why combining them catches what neither alone can.

### Layer 2 — Cell Tower Triangulation + Speed Check

Android logs cell tower IDs continuously alongside GPS. Tower IDs require physical radio proximity — they cannot be faked by a spoofing app. We cross-reference the last 3 session tower IDs against the disruption zone's coverage map.

On top of this: implied speed between consecutive GPS pings. If it exceeds 120 km/hr in an urban zone, the device teleported — it didn't travel. This check runs in < 1ms.

| Signal | Genuine Worker | Spoofer |
|--------|---------------|---------|
| Delivery platform shows offline | ✅ Yes | ❌ Usually still delivering |
| GPS in disruption zone | ✅ Real | ✅ Faked |
| Cell tower in disruption zone | ✅ Yes | ❌ Real tower exposed |
| Speed between GPS pings | ✅ Plausible | ❌ Teleport speed |
| Session in zone 2+ hrs before event | ✅ Consistent | ❌ Sudden appearance |

### Layer 3 — ML Anomaly Detection (Phase 3)

Isolation Forest on 12 features including platform account tenure, zone delivery consistency, claim frequency vs. peers, device uniqueness, and claim timing patterns. Upgrades to supervised Random Forest as labelled fraud data accumulates.

### Layer 4 — Fraud Ring Graph Detection (Phase 3)

Bipartite graph of worker accounts, device fingerprints, and UPI payout destinations. Any device or UPI node connected to more than 2 worker accounts is auto-escalated — coordinated rings are structurally visible even when individual claims look clean.

### UX — No Honest Worker Gets Punished

Bad weather degrades GPS signal and cell tower connectivity — the exact conditions that produce false positives. Our routing separates *technical signal failures* from *behavioural fraud*:

**Grace-Pay:** Flagged only for weak network signal (not device or behavioural anomalies) → payout fires immediately. Internal async review within 24 hours. Worker sees nothing except their money arriving. Pay first, verify after — because the alternative is systematically delaying payouts to workers during the storm that triggered the payout.

**Soft-Hold:** Zone mismatch detected → app prompts: *"Signal was unclear. Tap to confirm you were working in Zone 4."* One tap closes 90%+ of cases within 30–45 minutes.

| What Happened | Worker Sees | Backend Does |
|--------------|------------|--------------|
| Clean pass | "₹408 transferred. Stay safe." | Score logged |
| Network signal weak | "₹408 transferred. Stay safe." | Async review queued |
| Zone mismatch | "Confirming your location — payout in ~30 min." | ML rescores with fresh cell data |
| Anomaly detected | "We're reviewing this — update in 2 hours." | Manual review queue |
| Confirmed fraud | "Account paused. Contact support." | Flagged, policy voided |

The word "fraud" never appears in messages to the first four categories.

---

## 📊 Business Viability

### Unit Economics Per Worker Per Week

| Item | Amount | % of Premium |
|------|--------|-------------|
| Premium collected (avg, mid-risk worker) | ₹47 | 100% |
| Expected payout | ₹28 | ~60% |
| Fraud buffer | ₹5 | ~10% |
| Operating costs (API calls, infra, support) | ₹8 | ~17% |
| **Gross profit per policy** | **~₹6** | **~13%** |

**Payout frequency basis:** A mid-risk worker (Hyderabad) experiences ~10–12 qualifying disruptions per year. Per-trigger payout at ₹102 × 4 hrs = ₹408. Expected weekly payout: ~₹408 × (11/52) ≈ ₹86 for that profile, blended to ₹28 across the full mix of low-risk cities.

**Why the loss ratio holds:** Our dual-source trigger gate prevents false payouts from API glitches — a key driver of loss ratio overrun in other parametric products. Our delivery activity cross-validation reduces fraudulent claims from the industry average of ~25% to an estimated 8–10%, saving roughly ₹5–6 per worker per week in fraud costs. Both mechanisms work together to keep us at or below the 65% target.

### Break-Even Analysis

| Metric | Value |
|--------|-------|
| Gross profit per policy/month | ~₹26 (₹6 × 4.3 weeks) |
| Estimated fixed costs (team + infra) | ~₹8–10 lakh/month |
| Policies needed to break even | ~35,000–40,000 active policies |
| Path to break-even | 8–12 months post-launch with a 50,000-rider city pilot |

### Revenue Scaling Path

| Milestone | Active Workers | Monthly Revenue |
|-----------|---------------|----------------|
| Phase 2 pilot (1 city) | 1,000 | ~₹2 lakh |
| 6-month target (3 cities) | 15,000 | ~₹30 lakh |
| Year 1 (5 cities) | 50,000 | ~₹1 crore |
| Year 2 (all metros) | 2,00,000 | ~₹4 crore |

---

## 🛠️ Tech Stack

### Phase 1 — Running Now

| Layer | Choice | Reason |
|-------|--------|--------|
| Frontend | React 18 + Vite 5 | Smallest bundle, fastest HMR, ideal for PWA |
| State | React Context API | Sufficient scope — no Redux overhead |
| Weather | OpenWeatherMap (free tier) | Live rain, temp, AQI, visibility; local mock fallback |
| Font | Noto Sans | Latin + Tamil + Telugu + Devanagari from one file |

### Phase 2 — Being Built

| Layer | Choice | Reason |
|-------|--------|--------|
| Backend | **FastAPI (Python)** | Async, native Python ML integration, auto-Swagger, faster than Node.js/Express for ML-heavy workloads |
| Database | **PostgreSQL 16 + PostGIS** | ACID compliance for financial records; PostGIS for 500m-grid geospatial queries |
| Cache | **Redis 7** | Sub-millisecond lookups, rate limiting, trigger state |
| Event Bus | **Apache Kafka** | Decouples trigger detection from payout pipeline — a slow Razorpay response can't block claim detection |
| Auth | Twilio SMS OTP | Real OTP — no dependency on email |
| Partner Verification | Swiggy / Zomato Partner ID API (mock in Phase 2, real partnership Phase 3) | Proves active worker status, extracts zone + tenure — no UIDAI dependency |
| Payments | Razorpay (test mode) | UPI AutoPay mandate + instant payout |
| Notifications | WhatsApp Business API | Workers already have it open; higher open rate than push on low-RAM devices |
| Traffic | TomTom Traffic API | Real-time zone-level speed data for gridlock trigger |

### Phase 3 — Planned

| Layer | Choice | Reason |
|-------|--------|--------|
| ML Premium | XGBoost + LightGBM ensemble | 12% better AUC-ROC, 40% less memory vs single model |
| ML Forecast | TensorFlow LSTM | 72-hr predictive risk |
| ML Fraud | Isolation Forest → Random Forest | Unsupervised Phase 2, supervised Phase 3 |
| Inference | ONNX Runtime | < 50ms serving |
| Observability | Grafana + Prometheus | Loss ratio dashboards, trigger latency |
| Logs | ELK Stack | Audit trail for regulated financial product |
| Scale | Kubernetes (GKE) | Auto-scale during monsoon claim spikes |

---

## 🏗️ System Architecture

```
┌──────────────────────────────────────────────────────────────────────┐
│                     EXTERNAL DATA SOURCES                            │
│  OWM · AQICN · IMD RSS · NDMA · TomTom · NewsAPI · HTTP Probes      │
└──────┬─────────────┬──────────┬────────┬──────────┬─────────────────┘
       └─────────────┴──────────┴────────┴──────────┘
                           │ polls every 5 min · dual-source gate
                           ▼
┌──────────────────────────────────────────────────────────────────────┐
│           BACKEND — FastAPI · Python · Async                         │
│  ┌──────────────────────┐  ┌────────────────────────────────────┐   │
│  │  REST API  (port 8000)│  │  Trigger Monitor                   │   │
│  │  /api/v1/            │  │  cron · 8-trigger engine · Kafka   │   │
│  └──────────┬───────────┘  └───────────────┬────────────────────┘   │
└─────────────┼────────────────────────────  ┼───────────────────────┘
              │                              │
   ┌──────────▼─────────┐     ┌─────────────▼──────────────────┐
   │  FRONTEND           │     │  ML SERVICE — FastAPI/Python    │
   │  React 18 + Vite 5  │     │  XGBoost + LightGBM + SHAP     │
   │  PWA · < 150KB JS   │     │  IForest + ONNX (Phase 3)      │
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

One Python runtime spans both Backend and ML Service — no serialization overhead. ML models load once at startup and run as local function calls, not HTTP requests. Model inference overhead: < 5ms.

---

## 📅 Development Plan

**Phase 1 — Seed (March 4–20) ← Current**
- [x] Problem research — 2025 EPH data, partner counts, income loss statistics
- [x] Persona built around real device constraints (Redmi A2, 2 GB RAM, Jio 4G)
- [x] 7 real-world disruption scenarios including fog and traffic gridlock
- [x] 8 IMD/CPCB-calibrated triggers with dual-source confirmation gate
- [x] 5-component weighted premium formula with loyalty discount and tier structure
- [x] SHAP explainability layer for premium transparency
- [x] XGBoost + LightGBM ensemble with 47-feature input spec
- [x] Multi-layer fraud detection including delivery activity cross-validation
- [x] Cell tower triangulation + impossible-speed GPS check
- [x] Grace-Pay and Soft-Hold UX routing
- [x] Business viability with unit economics and break-even analysis
- [x] Low-end Android constraints — battery < 3%/day, data < 40 MB/month
- [x] FastAPI + PostGIS + Redis + Kafka architecture
- [x] Figma prototype — 8 screens
- [ ] 2-minute strategy video — replace `[Watch here](#)` above

**Phase 2 — Scale (March 21–April 4)**
- [ ] FastAPI backend + PostgreSQL 16 + PostGIS schema
- [ ] Twilio OTP + Swiggy/Zomato Partner ID verification — full registration flow (mocked in Phase 2)
- [ ] 8-trigger Trigger Monitor — 5-minute cron, dual-source gate, Kafka
- [ ] Delivery activity cross-validation layer (platform API mock)
- [ ] XGBoost + LightGBM premium model + SHAP explainability
- [ ] Razorpay UPI AutoPay + sandbox payout + WhatsApp notification
- [ ] React PWA — onboarding, policy purchase, live dashboard (< 150 KB JS)
- [ ] 2-minute demo video

**Phase 3 — Soar (April 5–17)**
- [ ] Isolation Forest fraud model live pre-payout
- [ ] Cell tower validation + impossible-speed check
- [ ] Graph-based fraud ring detection
- [ ] LSTM 72-hr predictive risk forecast
- [ ] Live Disruption Zone visualization on worker dashboard
- [ ] Admin dashboard — loss ratio, heatmap, manual review queue
- [ ] Worker dashboard — payout history, active coverage, zone status
- [ ] Kubernetes auto-scaling
- [ ] Final 5-minute video + pitch deck PDF

---

## 💡 What We're Planning Next

**Accessibility (Phase 2)**
WhatsApp as primary notification channel — works on 2G, no background persistence, lower battery. USSD/SMS fallback for Tier 2/3 workers without data plans.

**Smarter pricing (Phase 2)**
500m grid pricing via PostGIS — a worker on elevated ground pays ₹2–3 less than a worker 1 km away in a waterlogged zone. Loyalty discount compounds 3% per continuous quarter.

**Zone Consensus Trigger (Phase 3)**
When 5+ workers in the same 2 km radius all go offline simultaneously — detected via delivery activity drops — our system treats this as a disruption signal even before API thresholds are crossed. Anti-collusion: workers must be > 300m apart (verified via cell tower data), must have unique device fingerprints, and must have active delivery history in that zone. This catches hyperlocal events city-level APIs completely miss — a waterlogged lane, a blocked intersection, a surprise rally.

**Compound disruptions (Phase 3)**
When rain and a curfew hit simultaneously, the current model pays the higher trigger. A combined formula reflecting compounded income loss is on our backlog.

**Pre-emptive alerts (Phase 2)**
LSTM warns workers 3–6 hours before a trigger fires — *"Heavy rain likely this evening. Your coverage is active."* Builds trust before a payout is ever needed.

**Savings layer (Phase 4)**
In periods with no claims, a small percentage of the premium accumulates in a micro-savings reserve the worker can withdraw after 6 months of continuous enrollment.

---

## 👥 Team

| Name | Role | What They Own |
|------|------|--------------|
| **Irfan Hussain** | Team Lead & Architect | System design, product strategy, API architecture, ML pipeline |
| **Mahesh Sai** | Backend Engineer | FastAPI, PostgreSQL + PostGIS, Razorpay, trigger monitor |
| **Ahamad** | AI/ML Engineer | XGBoost + LightGBM + SHAP, fraud scoring, LSTM forecasting |
| **Akhil** | Frontend & DevOps | React/Vite PWA, low-end Android performance, Docker, Kubernetes |

---

> **Built for Guidewire DEVTrails 2026 · In partnership with EY & NIA**
>
> *Protecting India's 15+ lakh delivery partners — one parametric trigger at a time.*
>
> Target: DEVSummit Bangalore · May 2026 · Prize Pool: ₹6,00,000
