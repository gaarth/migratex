# 🛡️ Self-Healing Support Agent Dashboard (MigrateX)

![Next.js](https://img.shields.io/badge/next.js-%23000000.svg?style=for-the-badge&logo=next.js&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)
![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/tailwindcss-%2338B2AC.svg?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Framer Motion](https://img.shields.io/badge/Framer-Black?style=for-the-badge&logo=framer&logoColor=white)

A production-grade, human-in-the-loop (HITL) Self-Healing Support Agent Dashboard built with Next.js, Supabase, and Mistral AI. This system autonomously ingests events, analyzes patterns using AI, evaluates risk, and proposes or executes self-healing actions to resolve issues before they escalate.

---

## ✨ Key Features

- **🤖 Autonomous AI Pipeline**: An 8-step agent pipeline (Observe → Synthesize → Hypothesize → Evaluate → Decide → Recommend → Learn → Execute) powered by Mistral AI.
- **📊 Real-Time Dashboard**: Live metric cards tracking ingested events, active observations, high-risk issues, and pending approvals.
- **🌊 Live Activity Feed**: A real-time stream of system events, agent decisions, and action executions.
- **🚦 Human-in-the-Loop (HITL) Governance**: A robust approval queue for high-risk actions. The AI proposes solutions, but humans retain ultimate execution authority when necessary.
- **🎛️ Interactive Simulation Engine**: A 3-step wizard to simulate various production issues (e.g., Checkout Failures, Doc Gaps) with configurable intensity and risk profiles.
- **📈 Pipeline Visualizer**: An animated, 8-step stepper to visually track the agent's thought process and execution in real-time.

---

## 🏗️ Architecture Overview

The application is structured into three main layers: the UI Dashboard (React/Next.js/Framer Motion), the API & Agent Layer (Next.js Serverless), and the Database (Supabase PostgreSQL).

```text
┌─────────────────────────────────────────────────────────────────┐
│                       DASHBOARD UI (React)                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
│  │  Simulation │  │  Pipeline   │  │    Live Activity Feed   │  │
│  │    Modal    │  │  Visualizer │  │  + Approval Queue       │  │
│  └─────────────┘  └─────────────┘  └─────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                     API LAYER (Next.js)                         │
│                                                                 │
│  /api/dashboard/simulate   →  Generate events + trigger agent   │
│  /api/dashboard/stats      →  Real-time metrics from Supabase   │
│  /api/dashboard/activity   →  Activity feed + observations      │
│  /api/dashboard/approve/   →  Human-in-the-loop approvals       │
│  /api/agent-loop           →  Execute autonomous pipeline       │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      SUPABASE DATABASE                          │
│                                                                 │
│  raw_events       │  observations    │  hypotheses              │
│  risk_assessments │  decisions       │  action_proposals        │
│  human_approvals  │  audit_logs                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 💻 Tech Stack

- **Framework**: [Next.js 16](https://nextjs.org/) (App Router, React 19)
- **Language**: TypeScript
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/) & [Framer Motion](https://www.framer.com/motion/)
- **UI Components**: [Radix UI](https://www.radix-ui.com/) & [Lucide Icons](https://lucide.dev/)
- **Database & Auth**: [Supabase](https://supabase.com/)
- **AI Agent**: [Mistral AI API](https://mistral.ai/)
- **Charts**: [Recharts](https://recharts.org/)

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v20+ recommended)
- A Supabase Project
- A Mistral AI API Key

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd migratex
```

### 2. Install dependencies
```bash
npm install
# or yarn install / pnpm install / bun install
```

### 3. Set up Environment Variables
Create a `.env.local` file in the root directory and add the following configurations:
```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key

# Mistral AI API Key for autonomous hypothesis generation
MISTRAL_API_KEY=your_mistral_api_key
```

### 4. Database Setup
Ensure your Supabase project is set up with the required tables to run the dashboard. The following core entities govern the data flow:
- `raw_events`, `observations`, `hypotheses`, `risk_assessments`, `decisions`, `action_proposals`, `human_approvals`, `audit_logs`

*(Apply the database migrations found in the `/supabase/migrations/` folder using the Supabase CLI if applicable)*

### 5. Run the Development Server
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

---

## 🎮 How to Demo

The platform includes a built-in event simulator to rigorously test the agent's capabilities:

1. Navigate to the dashboard at `http://localhost:3000/dashboard`
2. Click the **Start Simulation** button on the top status bar.
3. Configure the simulation via the wizard:
   - **Scenario**: Select an issue scenario (recommend choosing *Mixed* for a diverse set of events).
   - **Risk Profile**: Select the risk level (recommend choosing *High* to observe the human-in-the-loop approval workflow).
   - **Intensity**: Set the scale of the simulation events.
4. Click **Start Simulation**.
5. Watch the **Pipeline Visualizer** animate across steps sequentially as the agent processes the generated events.
6. View real-time updates in the **Live Activity Feed**.
7. Observe the **Approval Queue**. Review High-Risk actions and engage with the Approve/Reject workflow directly from the UI.

---

## 🗺️ Autonomous Agent Pipeline Steps

The system processes events using a highly structural operational flow:

1. **OBSERVE**: Cluster raw systemic events into cogent observations.
2. **SYNTHESIZE**: Enrich events with contextual and historical data.
3. **HYPOTHESIZE**: Generate primary root causes via Mistral AI analysis.
4. **EVALUATE**: Attribute and score risk severity.
5. **DECIDE**: Classify priority dynamically and assert confidence scores.
6. **RECOMMEND**: Formulate structured propositions (e.g., dispatch emails, escalate tickets, self-heal).
7. **LEARN / EXECUTE**: Finalize human reviews, log outcomes into the audit trail, and execute the final resolutions.

---

## 📄 License
This project is licensed under the MIT License.
