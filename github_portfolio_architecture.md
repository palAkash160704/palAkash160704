# GitHub Portfolio Architecture

> [!NOTE]
> This document defines the structural engineering of Akash Pal's GitHub portfolio. It transforms the account from a simple code repository into a cohesive, production-grade engineering portfolio optimized for technical recruiters and senior engineering leaders.

---

## 1. Portfolio Hierarchy

To ensure a recruiter or engineering manager can instantly understand your capabilities, your repositories will be organized into strict categories. Repositories should utilize GitHub's "Topics" feature to maintain this hierarchy.

1. **Core Production Systems (`portfolio-core`):** High-impact, enterprise-grade projects (e.g., `Sentinel-QA`).
2. **AI & Agentic Orchestrations (`ai-agents`):** Complex LLM and multi-agent systems (e.g., `TripAI`).
3. **Computer Vision & ML (`cv-ml`):** Specialized modeling and vision systems (e.g., `ARGUS`).
4. **Full-Stack Engineering (`full-stack`):** End-to-end applications demonstrating UI/UX and API design (e.g., `AI-Startup-Validator`, `SkyCast`).
5. **Research & Learning (`research`, `system-design`):** Future repositories containing distributed systems labs, architecture notes, and algorithm optimizations.
6. **Archived / Deprecated (`archived`):** Old learning projects (set to Read-Only/Archived state so they don't dilute the portfolio).

---

## 2. Pinned Repositories Strategy

You have exactly 6 slots for pinned repositories. They must tell a cohesive story of your progression from Full-Stack to Complex AI/Backend Engineering.

| Order | Repository | Rationale for Pinning |
| :--- | :--- | :--- |
| **1** | `Sentinel-QA` | **The Crown Jewel:** Immediately proves enterprise-level capability, HPE experience, and mastery of cutting-edge Agentic AI and LangGraph. |
| **2** | `TripAI` | **The Orchestrator:** Showcases complex multi-agent interactions, real-time data streaming (SSE), and robust FastAPI backend architecture. |
| **3** | `ARGUS` | **The Specialization:** Proves deep technical capability beyond LLMs by showcasing YOLOv11, spatial tracking, and physics engine integration. |
| **4** | `AI-Startup-Validator` | **The Full-Stack Proof:** Demonstrates ability to build a complete product lifecycle (React to Node.js to LLaMA), proving versatility. |
| **5** | `SkyCast` | **The UI/UX Polish:** Proves frontend competency and capability to integrate efficiently with third-party APIs (Open-Meteo). |
| **6** | `distributed-systems-lab` *(Future)* | **The Foundation:** A highly technical repository detailing system design, Kubernetes, and backend scaling, proving you are a true Backend Engineer. |

---

## 3. Repository Ecosystem Design

### A. Sentinel-QA
- **Purpose:** Production-grade Agentic AI Testing Framework.
- **Target Audience:** Senior Backend Engineers, QA Architects, AI Researchers.
- **Difficulty Level:** Advanced / Enterprise.
- **Category:** Core Production Systems.
- **Primary Technologies:** LangGraph, FastAPI, ChromaDB, Python.
- **GitHub Topics:** `agentic-ai`, `langgraph`, `rag`, `fastapi`, `automated-testing`, `security`.
- **Expected Documentation:** High-level agent orchestration diagrams, ChromaDB schema, security protocol specifications.
- **Open Graph Preview:** Dark slate background with a glowing neon-green interconnected shield.

### B. TripAI
- **Purpose:** Multi-Agent AI travel planner utilizing real-time SSE.
- **Target Audience:** Full-Stack Engineers, AI Integrators.
- **Difficulty Level:** Advanced.
- **Category:** AI & Agentic Orchestrations.
- **Primary Technologies:** FastAPI, React, Ollama.
- **GitHub Topics:** `multi-agent`, `fastapi`, `react`, `ollama`, `server-sent-events`.
- **Expected Documentation:** Data flow diagram showing async SSE streaming, agent responsibility matrix.
- **Open Graph Preview:** Midnight blue background with a minimalist node-graph mapping a route.

### C. ARGUS
- **Purpose:** Context-aware multimodal surveillance with spatial tracking.
- **Target Audience:** Computer Vision Engineers, ML Researchers.
- **Difficulty Level:** Advanced / Specialized.
- **Category:** Computer Vision & ML.
- **Primary Technologies:** YOLOv11, ST-GCN, Physics Engine.
- **GitHub Topics:** `computer-vision`, `yolov11`, `pose-estimation`, `surveillance`.
- **Expected Documentation:** Model accuracy metrics, physics engine integration logic, hardware requirements.
- **Open Graph Preview:** Pitch black with an amber/gold 3D wireframe bounding box.

### D. AI Startup Validator
- **Purpose:** Full-stack AI platform to validate and scope business concepts.
- **Target Audience:** Product Engineers, Open Source Contributors.
- **Difficulty Level:** Intermediate / Advanced.
- **Category:** Full-Stack Engineering.
- **Primary Technologies:** React, Node.js, LLaMA.
- **GitHub Topics:** `full-stack`, `react`, `nodejs`, `llama`, `rest-api`.
- **Expected Documentation:** REST API endpoint tables, frontend component architecture.
- **Open Graph Preview:** Dark slate with a sleek purple line-chart transforming into a node.

### E. SkyCast
- **Purpose:** High-performance, responsive weather forecasting UI.
- **Target Audience:** Frontend Developers, UI/UX Designers.
- **Difficulty Level:** Intermediate.
- **Category:** Full-Stack Engineering.
- **Primary Technologies:** HTML, CSS, JavaScript, Open-Meteo.
- **GitHub Topics:** `frontend`, `weather-api`, `javascript`, `ui-ux`.
- **Expected Documentation:** Lighthouse performance scores, CSS methodology.
- **Open Graph Preview:** Deep navy with a cyan geometric radar wave.

---

## 4. Repository Naming Standard

Repositories must look like official software products.

- **Rule:** Use clean PascalCase (`TripAI`, `SkyCast`) or capitalized acronyms (`ARGUS`, `Sentinel-QA`). Alternatively, for purely technical/backend repos, use clean kebab-case (`distributed-systems-lab`).
- **Never Use:** Underscores (`_`), camelCase (`tripAi`), generic numbers (`project123`), or status suffixes (`_final`, `_v2`, `_test`).
- **Description:** Every repo MUST have a concise, 1-2 sentence description configured in the GitHub settings (not just the README).
- **Website URL:** Every repo MUST have the "Website" field filled in GitHub settings (link to live demo, or if none, link back to the repo itself or documentation).

---

## 5. Branch Strategy

Treat every personal project as if it is managed by a full engineering team.

- `main` / `master`: The production-ready, stable state. Only updated via Pull Requests.
- `develop`: The active integration branch (optional for smaller projects, vital for complex ones like Sentinel-QA).
- `feature/[feature-name]`: Used for building new capabilities (e.g., `feature/rag-integration`).
- `hotfix/[issue-name]`: Used for critical bug fixes in production.
- `release/v[X.X.X]`: Used when preparing for a semantic version release.

---

## 6. Release Strategy

Prove your capability to maintain software lifecycles.

- **Semantic Versioning:** Use `v[Major].[Minor].[Patch]` (e.g., `v1.2.0`).
- **GitHub Releases:** Do not just push to `main`. Create official GitHub Releases using the "Draft a new release" feature.
- **Release Notes:** Every release must auto-generate release notes detailing `Features`, `Bug Fixes`, and `Breaking Changes`.
- **Changelog:** Maintain a `CHANGELOG.md` following the "Keep a Changelog" standard.

---

## 7. Documentation Standard

Every production-grade repository in your ecosystem MUST contain the following files at the root level:

| File | Purpose |
| :--- | :--- |
| `README.md` | The comprehensive guide based on the Universal Template. |
| `LICENSE` | Standard MIT or Apache 2.0 license file. |
| `CONTRIBUTING.md` | Clear instructions on how others can fork, run, and submit PRs to your project. |
| `CODE_OF_CONDUCT.md` | Standard Contributor Covenant file (proves open-source professionalism). |
| `CHANGELOG.md` | Chronological list of user-facing changes per semantic version. |
| `SECURITY.md` | Instructions on how to responsibly disclose security vulnerabilities. |
| `.github/ISSUE_TEMPLATE/` | YAML or MD templates for `Bug Report` and `Feature Request`. |
| `.github/PULL_REQUEST_TEMPLATE.md`| A checklist template ensuring PRs meet your code quality standards. |

---

## 8. Expected Folder Organization

While frontend and backend structures differ, enforce this core standard across all apps:

```text
├── .github/                # All CI/CD workflows and PR/Issue templates
├── docs/                   # Deep-dive documentation and architecture diagrams
├── src/                    # Primary source code (or `app/`, `core/`)
├── tests/                  # Unit, Integration, and E2E tests
├── .env.example            # Empty template for required environment variables
├── .gitignore              # Standardized ignore file for the language
├── LICENSE                 # Legal
└── README.md               # Entrypoint
```
