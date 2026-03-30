# ⛽ FuelOps AI — Command Center

> **An AI-infused fuel operations management platform** for commercial fleets and fuel logistics. Track vessels, monitor fleet efficiency, analyze costs, and get real-time AI recommendations — all in one dark-mode command center.

![FuelOps AI](https://img.shields.io/badge/Powered%20by-Claude%20AI-orange?style=flat-square)
![HTML](https://img.shields.io/badge/Built%20with-HTML%20%2F%20CSS%20%2F%20JS-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)

---

## 🖥️ Preview

The dashboard features a full-screen industrial dark UI with real-time metrics, animated world maps, fleet tables, and a Claude-powered AI chat advisor — designed for fuel operations managers, logistics teams, and fleet administrators.

---

## ✨ Features

### 📊 Dashboard
- Live metrics: total fuel dispensed, daily cost, active vehicles, anomaly count
- Consumption breakdown bar charts by vehicle type (Heavy Truck, Van, Light, Equipment)
- Fleet efficiency score vs target
- Real-time fuel price tracker (Diesel, Unleaded, Premium, DEF)
- Tank level gauges (Tank A / B / C with color-coded thresholds)

### 🚛 Fleet Status
- Full vehicle roster with 62-unit tracking
- Per-unit actual vs target MPG comparison
- Gallons consumed, mileage, driver assignment
- Color-coded status badges: **Optimal**, **Review**, **Critical**

### 🚢 Ship Container Tracking
- Live animated SVG world map with continent outlines and sea lane routes
- 8 fuel tanker vessels tracked across 6 global shipping routes
- Vessels: VLCC Tankers, LNG Carriers, Aframax, Suezmax, Panamax
- Routes: Persian Gulf → Rotterdam (Cape & Suez), Houston → Rotterdam, Lagos → Rotterdam, Doha → Shanghai, Caracas → Houston, New Orleans → Rotterdam
- Real-time vessel position animation along route paths
- Per-container detail: cargo type, volume, speed, ETA, origin, destination, cargo value, progress
- Status tracking: In Transit, Delayed, Docked, Loading
- One-click **AI Analyze** routes container data directly into the AI advisor

### ⚠️ Alerts
- Severity-tiered alert system (Critical, Warning, Info)
- Pre-loaded anomalies: vessel weather delay, tank low-level warnings, budget forecast updates
- AI Diagnose / Advise / Plan buttons per alert
- Dismissable alert cards

### 🧮 Fuel Calculator
- Route fuel cost estimator with vehicle type selector
- Inputs: distance, vehicle type, custom MPG, fuel price, number of trips, load factor
- Live outputs: total cost, gallons, cost-per-mile, CO₂ emissions
- Weekly / monthly / annual projection engine
- **AI Optimize** button sends full route data to AI advisor

### 🤖 AI Advisor (Powered by Claude)
- Full conversational AI with deep fleet context baked into the system prompt
- Context fed: 62 vehicles, tank levels, live prices, anomalies, MTD spend
- 7 pre-built quick prompts covering: anomaly diagnosis, resupply timing, spend reduction, driver efficiency, weekly reports, price impact analysis, maintenance scheduling
- Supports multi-turn conversation with full history

### ⚙️ Configuration
- Adjustable alert thresholds (tank low %, MPG deviation %, daily budget ceiling)
- Live fuel price management per fuel type

---

## 🚀 Getting Started

### Prerequisites
- A modern web browser (Chrome, Firefox, Edge, Safari)
- An **Anthropic API key** for the AI Advisor feature

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/fuelops-ai.git

# Navigate into the folder
cd fuelops-ai

# Open in browser — no build step required
open fuel-ops-ai.html
```

Or simply drag `fuel-ops-ai.html` into any browser window.

### Enabling the AI Advisor

The AI Advisor calls the Anthropic API directly from the browser. To use it:

1. The app uses the `claude-sonnet-4-20250514` model via `https://api.anthropic.com/v1/messages`
2. If you are running this via **Claude.ai** (as an artifact), the API key is handled automatically
3. If self-hosting, you will need to proxy the API call through a backend server to keep your key secure — never expose your Anthropic API key in client-side code in production

#### Simple Node.js Proxy (optional for self-hosting)

```js
// server.js
const express = require('express');
const fetch = require('node-fetch');
const app = express();
app.use(express.json());
app.use(express.static('.'));

app.post('/api/chat', async (req, res) => {
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': process.env.ANTHROPIC_API_KEY,
      'anthropic-version': '2023-06-01'
    },
    body: JSON.stringify(req.body)
  });
  const data = await response.json();
  res.json(data);
});

app.listen(3000, () => console.log('FuelOps running on http://localhost:3000'));
```

```bash
ANTHROPIC_API_KEY=your_key_here node server.js
```

---

## 🗂️ Project Structure

```
fuelops-ai/
│
├── fuel-ops-ai.html       # Single-file application (HTML + CSS + JS)
└── README.md              # This file
```

Everything is contained in a single `.html` file — no frameworks, no build tools, no dependencies to install. The only external resources loaded are:

- **Google Fonts** — Space Mono (monospace) + DM Sans (UI)
- **Anthropic API** — for the AI Advisor chat

---

## 🛳️ Tracked Shipping Routes

| Vessel | Type | Route | Status |
|--------|------|--------|--------|
| FST-001 Atlantic Horizon | VLCC Tanker | Persian Gulf → Rotterdam (Cape) | 🟢 In Transit |
| FST-002 Pacific Pioneer | LNG Carrier | Persian Gulf → Yokohama | 🟢 In Transit |
| FST-003 Gulf Express | Aframax | Houston → Rotterdam | 🟢 In Transit |
| FST-004 West African Star | Suezmax | Lagos → Rotterdam | 🟡 Delayed |
| FST-005 Caribbean Carrier | Panamax | Caracas → Houston | 🔵 Docked |
| FST-006 Suez Star | VLCC Tanker | Persian Gulf → Rotterdam (Suez) | 🟢 In Transit |
| FST-007 Eastern Dragon | LNG Carrier | Doha → Shanghai | 🟢 In Transit |
| FST-008 Nordic Frost | Aframax | New Orleans → Rotterdam | ⚫ Loading |

---

## 🧠 AI System Context

The AI Advisor is pre-loaded with the following operational context on every session:

- Fleet composition: 62 vehicles across 4 types with per-type MPG targets
- Live tank levels: Tank A (78%), Tank B (34%), Tank C (12% critical)
- Current fuel prices: Diesel $3.42, Unleaded $3.18, Premium $3.65
- Active anomalies and their details
- Month-to-date spend vs budget
- Fleet efficiency score

This context is injected into the Claude system prompt so you can ask natural-language questions like:
> *"Why is TR-022 using so much diesel?"*
> *"When should I reorder premium fuel?"*
> *"What's the ROI of routing FST-004 around the storm?"*

---

## 🎨 Design System

| Token | Value |
|-------|-------|
| Background | `#0d0f12` |
| Surface | `#13161b` |
| Elevated | `#1a1e26` |
| Accent | `#f5a623` (amber) |
| Success | `#29c77a` |
| Danger | `#e85050` |
| Info | `#4a9eff` |
| Display font | Space Mono |
| UI font | DM Sans |

---

## 🔧 Customization

All fleet data, container data, and pricing is defined in JavaScript constants at the top of the `<script>` block. To adapt this for your own operations:

- **Fleet vehicles** — edit the `fleet-table` HTML rows in `page-fleet`
- **Containers** — edit the `CONTAINERS` array in the JS section
- **Fuel prices** — update the price values in the Configuration page or the dashboard HTML
- **AI context** — update the `SYSTEM` constant string with your real operational data
- **Alert thresholds** — adjust the Config panel defaults

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🙏 Acknowledgements

- Built with [Claude](https://claude.ai) by Anthropic
- Fonts by [Google Fonts](https://fonts.google.com)
- Inspired by industrial SCADA and logistics operations dashboards

---

*Built for fuel operations teams who need intelligence, not just data.*
