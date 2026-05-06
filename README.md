# ⬡ ArchLab — AI Architecture Diagram Generator

> **arch.eknathalabs.com** · Part of the [eknathalabs.com](https://eknathalabs.com) DevOps learning platform

Generate production-grade architecture diagrams for AWS, Azure, GCP, Kubernetes, CI/CD pipelines, Terraform IaC, Docker Compose, Network & Security, and Observability stacks — powered by Claude AI or fully offline.

---

## ✦ Features

### 🤖 AI Mode (Claude API)
- Describe any architecture in plain English — Claude Sonnet generates a precise, contextual diagram
- Intelligent component resolution with proper grouping, color coding, and edge labels
- Understands architecture intent, not just keywords

### ⚡ Offline Mode (Zero dependencies)
- 12 production-grade templates load instantly — no API key needed
- Keyword-based parser extracts services from free-text descriptions
- Works fully in-browser, no server required

### 🌙 Dark / Light Mode
- Auto-detects system preference (`prefers-color-scheme`) on first load
- Manual toggle via the 🌙/☀️ button in the header
- Preference persisted in `localStorage` across sessions
- Full theme re-renders SVG diagrams in correct light/dark colors — not just a CSS overlay

### 📱 Mobile-Optimized View
- Sidebar slides in/out as a bottom drawer on mobile (≤768px)
- Hamburger `☰` toggle in header, auto-closes when tapping the canvas
- Toolbar buttons shrink and scroll horizontally on small screens
- Diagram padding adapts to narrow viewports — works cleanly at 375px

### ▶ Step-by-Step Build Mode
- Click `▶ Steps` in the toolbar to open the build panel
- Reveals the architecture layer by layer, based on diagram groups
- Controls: **Prev**, **Play** (auto-advance every 1.2s), **Next**, layer chips for direct jump
- Progress bar tracks position through all layers
- Ideal for live presentations, tech talks, and teaching juniors

### 💥 Blast Radius Visualizer
- Click `💥 Blast` in the toolbar to activate crosshair mode
- Click any node — instantly see the full failure impact:
  - 🔴 **Red** outline — the failed component
  - 🟡 **Amber** outlines — all downstream dependents (BFS traversal)
  - 🔵 **Cyan** outlines — upstream dependencies
- Impact panel lists all affected services by name
- Dismiss with one click or deactivate blast mode

### 📐 Diagram Capabilities
- **9 platform targets:** AWS, Azure, GCP, Kubernetes, CI/CD, Terraform, Docker, Network/Security, Observability
- **12 built-in templates** covering the most common real-world patterns
- **Export:** SVG (vector), PNG (2× retina), DSL (human-readable text)
- **Views:** Visual diagram tab + DSL code tab
- Pure SVG rendering — no canvas, no third-party diagram libraries

---

## 🗂 Templates

| Template | Platform | Description |
|---|---|---|
| AWS 3-Tier Web App | AWS | Route53 → CloudFront → ALB → EC2 ASG → RDS Multi-AZ |
| AWS Serverless API | AWS | Cognito → API Gateway → Lambda → DynamoDB + SQS async |
| EKS Production Cluster | Kubernetes | NLB → Ingress → Istio → Microservices → Kafka → Postgres |
| Azure AKS Microservices | Azure | Front Door → APIM → AKS → Cosmos DB + Service Bus |
| GCP Data Platform | GCP | Pub/Sub → Dataflow → BigQuery → Vertex AI → Looker |
| GitHub Actions CI/CD | CI/CD | Push → Build → Trivy scan → Staging → Approval → Prod |
| Terraform IaC Graph | Terraform | Root module → VPC/EKS/RDS/S3 modules → Remote state |
| Docker Compose Stack | Docker | Nginx → React + Node.js API → Postgres + Redis + RabbitMQ |
| Full Observability Stack | Observability | OTel Collector → Prometheus + Loki + Jaeger → Grafana + Alertmanager |
| Zero Trust Network | Network | Cloudflare WAF → ZTNA → Okta MFA → Istio mTLS → Vault |
| AWS VPC Architecture | AWS | IGW → ALB → Public/Private subnets across 2 AZs → Transit GW |
| Kubernetes Microservices | Kubernetes | Ingress → Istio mesh → 5 services → Kafka → DBs per service |

---

## 🚀 Getting Started

###  Use the hosted version
Visit **[arch.eknathalabs.com](https://arch.eknathalabs.com)** — no setup needed.



## 🔑 API Key Setup (AI Mode)

1. Get a free API key at [console.anthropic.com](https://console.anthropic.com)
2. In ArchLab, paste your key (`sk-ant-api03-...`) into the **API KEY** field in the sidebar
3. Click **Save** — the key is stored in `localStorage` only, never sent anywhere except Anthropic's API
4. Ensure **AI Mode** is active via the toggle in the header

> **No API key?** Use **Offline Mode** — all 12 templates and the keyword parser work without any key.

---

## 📐 How It Works

### AI Generation Flow
```
User prompt
    │
    ▼
Claude Sonnet API (claude-sonnet-4-20250514)
    │   System prompt: structured JSON schema with
    │   node/edge/group definitions + platform color rules
    ▼
JSON: { title, groups[], nodes[], edges[] }
    │
    ▼
SVG Renderer (pure JS, theme-aware)
    │   layoutNodes() → group-aware grid layout
    │   renderSVG()   → nodes, edges, group boxes
    │                   re-renders with light/dark colors
    ▼
Inline SVG diagram
```

### Offline Keyword Flow
```
User prompt → token map lookup (AWS/Azure/GCP/K8s services)
           → generic phrase matching (Kafka, Grafana, Vault, …)
           → auto-edge generation
           → SVG Renderer
```

### Step-by-Step Layer Build
```
Diagram groups  →  Layer 1 (render group 1 only)
                →  Layer 2 (add group 2)
                →  Layer N (full diagram)
                    ↑ Play button auto-advances every 1.2s
                    ↑ Layer chips for direct navigation
```

### Blast Radius Algorithm
```
Click node X
    │
    ├─► BFS downstream  → collect all nodes X feeds into
    │                     (direct + transitive)
    │
    └─► BFS upstream    → collect all nodes that feed into X

Result:
  Red   = X (the failed node)
  Amber = downstream dependents
  Cyan  = upstream dependencies
```

### DSL Export Format
```
# Architecture: AWS 3-Tier Web App
# Platform: AWS
# Generated by ArchLab — arch.eknathalabs.com
# Mode: AI Generated

GROUPS:
  [g_edge] "Edge / CDN Layer"  color:#1a1800
  [g_private] "Private Subnet — App Tier"  color:#0d0020

NODES:
  (cf) "CloudFront CDN"  icon:☁  group:g_edge
  (alb) "Application Load Balancer"  icon:☁  group:g_public
  (ec2a) "EC2 Auto Scaling App Server (AZ-a)"  icon:☁  group:g_private

CONNECTIONS:
  cf --> alb
  alb --> ec2a [round-robin]
  alb --> ec2b [round-robin]
  ec2a --> rds_p [SQL]
```

---

## 🎮 Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + Enter` | Generate diagram from prompt |
| Click `▶ Steps` | Open step-by-step build panel |
| `← / →` in Steps panel | Navigate layers |
| Click `💥 Blast` then click node | Show blast radius |
| `☰` (mobile) | Toggle sidebar drawer |
| `🌙 / ☀️` | Toggle dark / light theme |

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML/CSS/JS — single file, zero build step |
| AI Backend | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| Diagram Rendering | Pure SVG, custom JS layout engine |
| Theme System | CSS custom properties + `prefers-color-scheme` |
| Fonts | JetBrains Mono + Syne (Google Fonts) |
| Hosting | GitHub Pages / Cloudflare Pages |
| Storage | `localStorage` for API key + theme preference only |

---

## 📁 Project Structure

```
arch.eknathalabs.com/
├── index.html          # Entire application (single file, ~98KB)
└── README.md           # This file
```

No dependencies. No npm. No build. One file.

---

## 🔗 Related Tools — eknathalabs.com

| Tool | URL | Description |
|---|---|---|
| KubeLab | kubelab.eknathalabs.com | Kubernetes learning lab |
| TerraformLab | terraform.eknathalabs.com | Terraform IaC reference |
| Linux Command Explainer | linux-command-explainer.eknathalabs.com | Linux command reference |
| GitHub Profile Analyzer | github-profile-analyzer.eknathalabs.com | GitHub portfolio analyzer |
| Interview Prep | interview-prep.eknathalabs.com | DevOps/Cloud interview prep |
| Resumelytics | resumelytics.eknathalabs.com | Resume analyzer |
| CI/CD Lab | cicd.eknathalabs.com | CI/CD pipeline reference |
| ChaosLab | chaoslab.eknathalabs.com | Chaos engineering playground |
| Docker Lab | docker.eknathalabs.com | Docker reference |
| Linux Lab | linux.eknathalabs.com | Linux for DevOps |
| Blog | blog.eknathalabs.com | DevOps articles |
| Learn | learn.eknathalabs.com | Learning paths |

---

## 🤝 Contributing

Contributions welcome — new templates, platform support, layout improvements, or bug fixes.

```bash
# Fork → clone → edit index.html → open PR
git checkout -b feat/new-template
git commit -m "feat: add GKE Autopilot template"
git push origin feat/new-template
```

**Adding a template** — each template is a JS object in the `TEMPLATES` map:

```javascript
myTemplate: {
  platform: 'aws',          // aws | azure | gcp | k8s | cicd | tf | docker | net | obs
  title: 'My Architecture',
  groups: [
    { id: 'g_1', label: 'Layer Name', color: '#1a1800' }
  ],
  nodes: [
    { id: 'n_1', label: 'Service\nSubtitle', icon: '☁', color: '#ff9900', group: 'g_1' }
  ],
  edges: [
    { from: 'n_1', to: 'n_2', label: 'HTTP' }
  ]
}
```

---

## 📋 Changelog

### v2.0
- ✦ Added **AI Mode** via Claude Sonnet API
- ✦ Added **Offline / AI mode toggle**
- ✦ Added quick prompt chips in empty state
- ✦ Export buttons disabled until diagram is ready

### v2.1 (current)
- ✦ **Dark / Light mode** with system `prefers-color-scheme` auto-detect
- ✦ **Mobile-optimized** sidebar drawer, responsive toolbar, touch-friendly layout
- ✦ **Step-by-step build mode** — layer-by-layer reveal with play/pause and progress bar
- ✦ **Blast radius visualizer** — BFS impact analysis with live SVG highlighting

---

## 📄 License

MIT — free to use, fork, and build on.

---

<div align="center">
  Built by <a href="https://eknathalabs.com">Eknatha Reddy</a> · <a href="https://github.com/eknatha">@eknatha</a>
  <br/>
  <sub>arch.eknathalabs.com · Part of the eknathalabs DevOps learning platform</sub>
</div>
