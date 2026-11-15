# Loopmates: Personal Autonomous AI Team

**A personal AI team that runs on your own computer.** You get a roster of 19 specialized AI agents, called **Mates**. Each one has a name, a mascot, a voice, a job, and a personality of its own. You can chat with them, delegate multi-step projects, call them by voice in real time, and let them autonomously watch your systems and contact you when something matters.

> **🏆 Submission for Build with Gemini, Chennai (MLH), Nov 14–15, 2026**  
> **Track:** Best Use of the Google Gemini API  
> **License:** [MIT License](LICENSE) · Built with Google Gemini & Anthropic Claude

---

## ⚡ Where Gemini is Used

Loopmates leverages the Google Gemini ecosystem across multiple core modalities:

| Feature | Gemini API / Capability | What it does |
|---|---|---|
| **Real-Time Voice Calls** | **Gemini Live API** (`BidiGenerateContent` over WebSocket) | Two-way, ultra-low latency voice calls with your Mates from the web dashboard or mobile app. Each Mate has a distinct voice. Mates can proactively call you when input is needed, or schedule call-backs ("call me at 6"). Post-call transcripts synthesize into chat history and follow-up tasks. |
| **Voice Previews** | **Gemini TTS** (`gemini-2.5-flash-preview-tts`) | Audio preview of each Mate's personality and voice timbre in the dashboard settings before assigning. |
| **Agent Reasoning Engine** | **Gemini 2.5 Flash** (OpenAI-compatible endpoint) | Core cognition: multi-turn chat, task decomposition, native tool calling, second-opinion verification, and executive summaries. |
| **Web Search Grounding** | **Gemini Search Grounding** | Research and Scout perform web lookups with grounded, verifiable, and cited sources. |
| **Semantic Long-Term Memory** | **`gemini-embedding-001`** | Semantic vector search across shared memories, per-agent journals, and reflection lessons. |
| **Deep Research Harness** | **Gemini 1M+ Long Context** | Reads uploaded PDFs, datasheets, and patent filings. Extracts structured values with source quotes, programmatically validated against source pages to eliminate hallucinations. |

---

## 🧠 What Loopmates Does

- **A Team, Not a Chatbot:** 19 built-in Mates (Research, Code, Writer, Planner, Ops, Mimo, Luna, Chef, Orbit, Zen...) plus custom agents you configure. Each Mate has an individual role card: operational guidelines, speech style, message sign-offs, trusted collaborators, and debate stances. `@mate` pulls one into a group chat, and a leader (Mimo by default) coordinates workflows.
- **Autonomous Runs:** Multi-step pipelines: Planner splits the work, dispatches steps to specialized Mates, a second-opinion Mate reviews each output with iterative feedback, risky actions wait for human approval, and an executive report is delivered. Coding steps can invoke Claude Code, Codex, or OpenCode in a sandbox supervised by the Code Mate.
- **Voice Calls & Phone Bridge:** Call any Mate, or let Mates ring you when an approval or decision is pending. Mates can schedule time-gated alerts. Full voice calls run through Gemini Live with audio previews and seamless transcript synchronization.
- **Nightly Self-Review & Reflection:** When the host machine is idle, each Mate audits its recent performance (failed tasks, rejected actions, user feedback). From this, it synthesizes **lessons** that dynamically augment future system prompts, and drafts new **skills** for user authorization.
- **Deep Research Harness:** Automatic extraction of verified claim tables, patent claim charts, and datasheets. Every extracted claim requires an exact string quote from the source document; unverified claims are explicitly categorized under "Dropped" to prevent AI hallucination.
- **Deterministic Python Sandbox:** Data, Code, and Byte execute short Python scripts (containerized in Docker when available) for accurate arithmetic, data cleaning, and data visualization. Every execution requires user confirmation.
- **Jarvis Monitoring Mode:** The coordinator Mate continuously watches deadlines, RSS feeds, YouTube transcripts, GitHub releases, and Home Assistant smart home devices. Events are scored and routed into morning briefings, instant messages, or emergency calls.
- **Memory & Personalization:** Shared facts, a dynamic knowledge graph, and per-Mate journals: when you request "shorter please", that specific Mate permanently adjusts its verbosity.
- **Company Mode:** Directory management, task assignments, and employee check-ins. Team members interact with the bot on Telegram and access only their authorized projects.
- **Omnichannel Access:** Responsive web dashboard, React Native mobile app (with push notifications), Telegram, Discord, Slack (Socket Mode), and WhatsApp (Cloud API).

---

## 🔌 Connected Integrations

All integrations are modular, optional, and configured via **Dashboard → Connections** with live test buttons.

| Integration | Capabilities |
|---|---|
| **Obsidian** | In-place read/write on local vaults; Luna journals into daily notes; wiki `[[links]]` populate the knowledge graph. |
| **Notion** | Search and read shared workspaces; publish plans, drafts, and documentation pages. |
| **Google Workspace** | Sandboxed Google Drive folder access; Google Calendar scheduling and free/busy lookup; Gmail search with **drafts-only** safety (never auto-sends). |
| **Slack** | Direct messaging and `@mention` in channels via Socket Mode (no public IP/webhook required); each Mate responds with its own avatar and name. |
| **WhatsApp** | Official Meta Cloud API integration for direct messaging and approval requests. |
| **Telegram & Discord** | Full chat, status notifications, interactive tap-to-answer confirmation cards, and voice call invite links. |
| **GitHub** | Repository watches, automated branch checkout, sandboxed coding runs, and Pull Request generation. |
| **Todoist & Linear** | Auto-generate to-do items, grocery lists, and sprint issues from execution plans. |
| **Spotify** | Tune analyzes your listening history and curates custom algorithmic playlists. |
| **Home Assistant** | Read sensor telemetry and trigger smart home devices. High-security entities (locks, alarms, garage doors) strictly mandate manual user approval. |
| **MCP Servers** | Connect any standard HTTP or stdio Model Context Protocol (MCP) server with granular per-agent tool permissions. |

---

## 🏗️ Architecture & Technology Stack

```
   Browser Dashboard (Next.js)      Mobile App (Expo)      Telegram · Discord · Slack · WhatsApp
               │                           │                              │
               └───────────── HTTPS (Cloudflare Quick Tunnel) ────────────┘
                                           │
               ┌───────────────────────────▼───────────────────────────┐
               │  Loopmates Server on YOUR Machine (Node.js Process)   │
               │  Agent loop · Fastify · Run engine · Scheduler        │
               │  Sandbox · Local browser · Gemini Live Audio Relay    │
               └───────────────┬───────────────────────────┬───────────┘
                               │                           │
                 Firebase Auth + Firestore           Google Gemini APIs
                 (Free Tier Cloud State)             Live WS · Flash · Search · Embeddings
```

| Layer | Location | Tech Stack & Security |
|---|---|---|
| `backend/` | Local host computer (service) | Node 22, Fastify, Firestore. Model keys, API secrets, and OAuth tokens are encrypted at rest with **AES-256-GCM**. |
| `dashboard/` | Vercel or local | Next.js 15, TypeScript, Tailwind CSS, Lucide. |
| `mobile/` | Android / iOS | Expo, React Native. |
| `app/`, `components/` | Web Root | Interactive landing page built with Next.js App Router and GSAP motion. |
| `design/` | Design system | Design tokens compiled to web and native targets via `tokens.json`. |
| `firestore.rules` | Firebase | Multi-tenant isolation: every record is constrained to the owner's authenticated UID. |

### Universal Model Provider Support
While Gemini serves as the primary intelligence and voice layer, Loopmates supports any OpenAI-compatible API with automatic failover:
- **Cloud Providers:** Google Gemini, OpenRouter, Groq, Cerebras, NVIDIA NIM, Together, DeepSeek, Mistral, OpenAI.
- **Local Self-Hosted:** Ollama, LM Studio, vLLM, LiteLLM.

```
Base URL:  https://openrouter.ai/api/v1      (or http://localhost:11434/v1 for Ollama)
API Key:   sk-...
Model:     any preferred model identifier
```

---

## 🛡️ Safety & Security Principles

1. **Local-First Secret Storage:** API keys, bot credentials, and OAuth tokens are stored locally on your machine, sealed with AES-256-GCM. The cloud dashboard and phone app only receive scoped Firebase session tokens.
2. **Explicit Human Approvals:** Any operation that deletes data, contacts external individuals, deploys code, spends money, or manipulates smart home physical security (locks, garage doors) requires interactive approval.
3. **Hardened Guardrails:** Agents are structurally blocked from entering payment card numbers, reading raw passwords, or accessing private intranet IPs (SSRF protection). Web scraping strictly adheres to `robots.txt`.
4. **Data vs. Instruction Segregation:** Outside text (emails, web scrapes, chat inputs) is strictly sandboxed as passive data to prevent prompt injection attacks.

---

## 🚀 Getting Started

### Prerequisites
- Windows or Linux PC (stays powered on for 24/7 background automations)
- **Node.js 22+**
- Free **Firebase** project (Authentication + Firestore)
- Free **Gemini API Key** from [Google AI Studio](https://aistudio.google.com/)

### 1. Configure Firebase
1. Create a Firebase project and enable Authentication (Google or Email/Password) and Cloud Firestore.
2. Deploy Firestore security rules:
   ```bash
   firebase deploy --only firestore:rules
   ```
   *(Alternatively, paste the contents of `firestore.rules` into the Firebase Console).*

### 2. Install the Local Server
```powershell
# Windows PowerShell (Run as Administrator or regular user)
cd backend
powershell -ExecutionPolicy Bypass -File .\install.ps1
```
```bash
# Linux
cd backend
chmod +x ./install.sh && ./install.sh
```
The installer provisions Node if missing, registers an auto-restarting background service, sets up the `loopmates` CLI, and launches the browser setup wizard.

### 3. Pair & Connect
1. On the local setup page, input your Firebase service account key and Gemini API key, then launch the Cloudflare tunnel.
2. Deploy `dashboard/` to Vercel with your Firebase web config (`NEXT_PUBLIC_FIREBASE_*`), sign in, and enter the one-time pairing PIN.
3. Enable integrations in **Dashboard → Connections**.

### 4. Run the Landing Page & Dashboard Locally
```bash
# Web Landing Page
npm install
npm run dev      # http://localhost:3000

# Web Dashboard
cd dashboard
npm install
npm run dev      # http://localhost:3001
```

---

## 🧪 Testing & Verification

```bash
# Backend unit tests and end-to-end integration tests
cd backend
npm test

# Browser automation engine smoke check
npm run test:browser

# Frontend type checks and production builds
cd ../dashboard
npx tsc --noEmit && npm run lint && npm run build

# Mobile type check
cd ../mobile
npm run typecheck
```

---

## 🌟 Built During Build with Gemini Hackathon (Nov 14–15, 2026)

Key innovations engineered during the hackathon weekend:
- **Nightly Reflection Loop (`backend/src/api/reflect.js`):** Autonomous agent post-mortem analysis that summarizes daily mistakes and writes self-correcting rules.
- **Deep Research Fact Verification (`backend/src/research/`):** Algorithmic verification that cross-references extracted technical specs against raw document text.
- **Gemini Live WebSocket Relay:** Low-latency bidirectional voice bridge between web/mobile clients and Gemini Live audio streaming.
- **Multi-Agent Standup Generator:** Asynchronous weekly standup compilation where each Mate synthesizes its work in its designated persona.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
