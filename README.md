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
- 24 production-grade templates load instantly — no API key needed
- Keyword-based parser extracts services from free-text descriptions
- Works fully in-browser, no server, no build step

### 🌙 Dark / Light Mode
- Auto-detects system preference (`prefers-color-scheme`) on first load
- Manual toggle via the 🌙/☀️ button in the header
- Preference persisted in `localStorage` across sessions
- Full theme re-renders SVG diagrams with correct light/dark colors — not just a CSS overlay

### 📱 Mobile-Optimized View
- Sidebar slides in/out as a drawer on mobile (≤768px)
- Hamburger `☰` toggle in header, auto-closes when tapping the canvas
- Toolbar buttons shrink and scroll horizontally on small screens
- Works cleanly at 375px iPhone width

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

### 🔍 Node Expand (click-to-expand)
- Click `🔍 Expand` in the toolbar to activate
- Click any node to open a detail modal showing:
  - Incoming and outgoing connections with edge labels
  - Layer/group membership
  - **AI explanation** — Claude Sonnet generates a 2-3 sentence technical description of the node's role in this specific architecture (requires API key; falls back to static description offline)
- Click backdrop or ✕ to dismiss

### 🎬 Sequence Diagram View
- A `Sequence` tab sits alongside `Diagram` and `DSL` in the toolbar
- Automatically derives a time-ordered sequence diagram from the architecture's edges
- Shows actors with lifelines, numbered messages, dashed return flows, activation boxes, and self-call loops
- Re-renders automatically when theme changes or a new diagram loads

### ⊟ Minimap
- Click `⊞ Map` toggle (bottom-right of diagram) after a diagram loads
- 140×90px canvas overview of the full diagram — group backgrounds, node boxes, edges
- Green viewport rectangle tracks your scroll position in real-time
- Re-renders on theme change and new diagram loads

### 📐 Diagram Capabilities
- **9 platform targets:** AWS, Azure, GCP, Kubernetes, CI/CD, Terraform, Docker, Network/Security, Observability
- **24 built-in templates** covering the most common real-world patterns
- **Export:** SVG (vector), PNG (2× retina), DSL (human-readable text)
- **Views:** Diagram · Sequence · DSL
- Pure SVG rendering — no canvas API, no third-party diagram libraries

---

## 🗂 Templates

### ☁ AWS (4 templates)

| Template | Key Services |
|---|---|
| **AWS 3-Tier Web App** | Route53 → CloudFront + WAF → ALB → EC2 ASG → RDS MySQL Multi-AZ + ElastiCache Redis |
| **AWS Serverless API** | Cognito → API Gateway → Lambda → DynamoDB + SQS + SNS + CloudWatch |
| **EKS Production Cluster** | NLB → Ingress → Istio → Microservices → Kafka → PostgreSQL + Redis + ArgoCD |
| **AWS VPC Architecture** | IGW → ALB → Public/Private subnets across 2 AZs → NAT Gateway → Transit GW + VPN |

### 🔷 Azure (5 templates)

| Template | Key Services |
|---|---|
| **Azure AKS Microservices** | Front Door → APIM → AKS → Cosmos DB + Service Bus + Key Vault + Monitor |
| **Azure 3-Tier Web App** | Front Door + WAF → CDN → App Service → Azure SQL + Cosmos DB + Redis |
| **Azure Serverless Event-Driven** | Azure AD B2C → APIM → Functions (HTTP/Event/Timer/Blob) → Event Hubs + Service Bus + Event Grid |
| **Azure Data Platform** | ADF + Event Hubs → ADLS Gen2 (Raw/Curated/Gold) → Databricks → Synapse + Power BI + Purview |
| **Azure DevSecOps Pipeline** | Azure Repos → Pipelines → SonarCloud + Defender + Checkov → ACR → AKS Staging → Approval → AKS Prod |

### 🌐 GCP (5 templates)

| Template | Key Services |
|---|---|
| **GCP Data Platform** | Pub/Sub → Dataflow → BigQuery → Vertex AI → Looker Studio + Cloud Composer |
| **GCP 3-Tier Web App** | Cloud Armor → CDN → Load Balancer → Cloud Run → Cloud SQL + Memorystore + Secret Manager |
| **GCP GKE Production** | GLB → Cloud Armor → GKE Ingress → Anthos Service Mesh → Microservices → Cloud SQL + Firestore |
| **GCP Serverless Event-Driven** | Firebase Auth → API Gateway → Cloud Functions → Pub/Sub + Eventarc → Firestore + BigQuery + Vertex AI |
| **GCP Data Engineering** | Datastream CDC + Pub/Sub → GCS Raw/Curated zones → Dataflow + Dataproc + dbt → BigQuery → Looker + Dataplex |

### ⎈ Kubernetes (5 templates)

| Template | Key Services |
|---|---|
| **K8s Microservices** | Ingress → Istio mesh → API GW + 4 services → Kafka → per-service DBs + ArgoCD + Prometheus |
| **K8s RBAC & Security** | OIDC → kube-apiserver → RBAC/ClusterRole → PSA + OPA Gatekeeper + NetworkPolicy → Vault + Falco |
| **K8s Multi-Tenant Platform** | Ingress + cert-manager + ArgoCD + KEDA → 3 isolated namespaces → Prometheus + Loki shared |
| **K8s Networking Deep Dive** | LoadBalancer → NodePort → NGINX Ingress → Gateway API → Cilium eBPF + Envoy mTLS + CoreDNS |
| **K8s Stateful Workloads** | CloudNativePG + Redis Operator + Strimzi Kafka → StatefulSets + PVCs → CSI Driver → Velero backup |

### Other (5 templates)

| Template | Platform | Key Services |
|---|---|---|
| **GitHub Actions CI/CD** | CI/CD | Push → Build → Trivy + SonarQube → Staging EKS → Approval → Prod EKS + PagerDuty |
| **Terraform IaC Graph** | Terraform | Root module → VPC/EKS/RDS/S3 modules → Remote state (S3 + DynamoDB lock) |
| **Docker Compose Stack** | Docker | Nginx → React + Node.js API → Postgres + Redis + RabbitMQ → Prometheus + Grafana |
| **Full Observability Stack** | Observability | OTel Collector → Prometheus + Loki + Jaeger → Grafana + Alertmanager → PagerDuty + Slack |
| **Zero Trust Network** | Network | Cloudflare WAF → ZTNA → Okta MFA → Policy Engine → Istio mTLS → Vault + Falco + SIEM |

---

## 🚀 Getting Started

###  Use the hosted version
Visit **[arch.eknathalabs.com](https://arch.eknathalabs.com)** — no setup needed.



## 🔑 API Key Setup (AI Mode + Node Expand AI)

1. Get a free API key at [console.anthropic.com](https://console.anthropic.com)
2. In ArchLab, paste your key (`sk-ant-api03-...`) into the **API KEY** field in the sidebar
3. Click **Save** — stored in `localStorage` only, never sent anywhere except Anthropic's API
4. Ensure **AI Mode** is active via the toggle in the header

> **No API key?** Use **Offline Mode** — all 24 templates, keyword parser, sequence diagrams, blast radius, minimap, and step-by-step mode all work without any key. The Node Expand modal falls back to a static description.

---

## 📐 How It Works

### AI Generation Flow
```
User prompt
    │
    ▼
Claude Sonnet API (claude-sonnet-4-20250514)
    │   System prompt enforces structured JSON schema:
    │   { title, groups[], nodes[], edges[] }
    ▼
JSON parsed and validated
    │
    ▼
SVG Renderer (pure JS, theme-aware)
    │   layoutNodes()  → group-aware grid layout
    │   renderSVG()    → nodes, edges, group boxes
    │                    stores positions globally
    ▼
Inline SVG + Minimap + Sequence + Blast + Expand
```

### Offline Keyword Flow
```
User prompt → token map lookup (AWS/Azure/GCP/K8s services)
           → generic phrase matching (Kafka, Grafana, Vault…)
           → auto-edge generation
           → SVG Renderer
```

### Sequence Diagram Derivation
```
Architecture edges (ordered)
    │
    ▼
Actors = diagram nodes (up to 8)
Lifelines drawn per actor
Each edge → numbered message arrow
Return/response edges → dashed arrow
Self-call edges → loop notation
```

### Blast Radius Algorithm
```
Click node X
    ├─► BFS downstream → all nodes X transitively feeds into → Amber highlight
    └─► BFS upstream   → all nodes that feed into X          → Cyan highlight
                          X itself                           → Red highlight
```

### Step-by-Step Layer Build
```
Groups → Layer 1 (group 1 nodes only)
       → Layer 2 (add group 2)
       → Layer N (full diagram)
         ↑ Play auto-advances every 1.2s
         ↑ Layer chips for direct jump
         ↑ Progress bar tracks position
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
  ec2a --> rds_p [SQL]
```

---

## 🎮 Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + Enter` | Generate diagram from prompt |
| Click `▶ Steps` | Open step-by-step build panel |
| `← / →` in Steps panel | Navigate layers |
| Click `💥 Blast` → click node | Show blast radius |
| Click `🔍 Expand` → click node | Open node detail modal |
| Click `Sequence` tab | Show sequence diagram |
| Click `⊞ Map` | Toggle minimap |
| `🌙 / ☀️` | Toggle dark / light theme |
| `☰` (mobile) | Toggle sidebar drawer |

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML/CSS/JS — single file, zero build step |
| AI Generation | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| AI Node Explain | Anthropic Claude API (inline, per node click) |
| Diagram Rendering | Pure SVG, custom JS layout engine |
| Sequence Diagrams | SVG, derived from architecture edge data |
| Minimap | HTML5 Canvas, real-time scroll sync |
| Theme System | CSS custom properties + `prefers-color-scheme` |
| Fonts | JetBrains Mono + Syne (Google Fonts) |
| Hosting | GitHub Pages / Cloudflare Pages |
| Storage | `localStorage` for API key + theme preference only |

---

## 📁 Project Structure

```
archlab/
├── index.html          # Entire application (~156KB, 2,916 lines)
│                         57 functions · 24 templates · 9 platforms
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



**Adding a template** — each template is a JS object in the `TEMPLATES` map:

```javascript
myTemplate: {
  platform: 'gcp',      // aws | azure | gcp | k8s | cicd | tf | docker | net | obs
  title: 'My Architecture',
  groups: [
    { id: 'g_1', label: 'Layer Name', color: '#00071a' }
  ],
  nodes: [
    { id: 'n_1', label: 'Service\nSubtitle', icon: '☁', color: '#4285f4', group: 'g_1' }
  ],
  edges: [
    { from: 'n_1', to: 'n_2', label: 'HTTP' }
  ]
}
```

Then add a sidebar button in the `<!-- Templates -->` section:
```html
<button class="tbtn" onclick="useTpl('myTemplate')">
  <span class="ti">☁</span>
  <span class="tname">My Architecture</span>
</button>
```

---

## 📋 Changelog

### v2.0
- ✦ AI Mode via Claude Sonnet API with structured JSON diagram generation
- ✦ Offline / AI mode toggle
- ✦ Quick prompt chips in empty state
- ✦ Export: SVG, PNG, DSL

### v2.1
- ✦ Dark / Light mode with `prefers-color-scheme` auto-detect
- ✦ Mobile-optimized sidebar drawer and responsive toolbar
- ✦ Step-by-step build mode with play/pause and layer navigation
- ✦ Blast radius visualizer with BFS impact analysis and SVG highlighting

### v2.2
- ✦ GCP architecture templates (5 total: Data Platform, 3-Tier, GKE, Serverless, Data Engineering)
- ✦ Azure architecture templates (5 total: AKS, 3-Tier, Serverless, Data Platform, DevSecOps)
- ✦ Kubernetes deep-dive templates (5 total: Microservices, RBAC & Security, Multi-Tenant, Networking, Stateful Workloads)

### v2.3 (current)
- ✦ **Sequence Diagram** tab — auto-derived from architecture edges, full SVG with lifelines, numbered steps, return flows
- ✦ **Node Expand modal** — click any node to see connections, group, and AI-generated explanation
- ✦ **Minimap** — real-time canvas overview with scroll-synced viewport indicator
- ✦ Platform button click fix — `pointer-events:none` on child spans + delegated listener
- ✦ Blast radius fix — mode toggle now immediately wires SVG click handler

---

## 📄 License

MIT — free to use, fork, and build on.

---

<div align="center">
  Built by <a href="https://eknathalabs.com">Eknatha Reddy Puli</a> · <a href="https://github.com/eknatha">@eknatha</a>
  <br/>
  <sub>arch.eknathalabs.com · Part of the eknathalabs DevOps learning platform</sub>
</div>
