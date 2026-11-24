# 🔬 Deep Research Agent UI

[![Next.js](https://img.shields.io/badge/Next.js-14.2.5-black?style=flat-square&logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-18-blue?style=flat-square&logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4.4-38B2AC?style=flat-square&logo=tailwind-css)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](#license)

A modern, editorial web application built with **Next.js 14 (App Router)** for interacting with an autonomous multi-node Deep Research Agent. 

The system coordinates specialized autonomous nodes (**Planner → Researcher → Critic → Writer**) to scour the web and ArXiv, cross-reference claims, detect contradictory evidence, and generate in-depth, citation-backed intelligence reports in real-time.

---

## ✨ Features

- **⚡ Real-Time Streaming & Progress Tracking**
  - Live WebSocket connection (`/reports/:id/stream`) displays streaming execution logs directly from the backend nodes.
  - Interactive multi-step visual indicator tracking the agent's active phase: `Queued` &rarr; `Researching` &rarr; `Critiquing` &rarr; `Writing` &rarr; `Complete`.
  - Automatic fallback polling ensures state synchronization even if WebSocket drops.

- **⚖️ Conflict Detection & Fact-Checking**
  - Dedicated conflict inspector highlighting claims where sources disagree.
  - Side-by-side comparison of conflicting sources with detailed contextual explanations produced by the Critic agent.

- **📚 Interactive Citation Explorer**
  - Full source attribution breakdown across **Web**, **ArXiv**, and **PDF** sources.
  - Confidence scoring meters and interactive drawer/modal for inspecting cited sources and original links.

- **📄 Export & Portability**
  - Export completed reports directly to **PDF** or **DOCX** with one click.
  - Single-click **Copy Markdown** for instant note-taking, sharing, or publishing.

- **🎨 Bespoke Editorial Aesthetic**
  - Sophisticated dark theme with custom typography (`Playfair Display`, `Inter`, and `IBM Plex Mono`).
  - Subtle noise texture overlay and fluid micro-animations powered by **Framer Motion**.

- **🛡️ Built-in Next.js Reverse Proxy**
  - Automatically proxies `/api/v1/*` requests to the backend service to prevent CORS issues in local development and production.

---

## 🛠️ Tech Stack

- **Framework**: [Next.js 14](https://nextjs.org/) (App Router, Server & Client Components)
- **Library**: [React 18](https://react.dev/)
- **Language**: [TypeScript](https://www.typescriptlang.org/)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) + PostCSS
- **Animations**: [Framer Motion](https://www.framer.com/motion/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **Networking**: [Axios](https://axios-http.com/) & Native WebSockets

---

## 📂 Project Structure

```text
research-agent-ui/
├── app/
│   ├── globals.css              # Custom styling, CSS theme variables, noise overlay
│   ├── layout.tsx               # Root layout, Google Fonts integration
│   ├── page.tsx                 # Home page: query submission & active/past reports
│   └── reports/
│       └── [id]/
│           └── page.tsx         # Report view: live logs, status, citations, export
├── lib/
│   └── api.ts                   # Axios client, WebSocket resolver, and TypeScript interfaces
├── .env.local.example           # Example environment configuration
├── next.config.js               # Next.js config with API proxy rewrites
├── tailwind.config.js           # Tailwind design tokens
├── tsconfig.json                # TypeScript compiler configuration
└── package.json                 # Dependencies and scripts
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js**: `v18.17.0` or higher
- **Package Manager**: `npm`, `yarn`, or `pnpm`
- **Backend Service**: A running instance of the Deep Research Agent API (typically running on `http://localhost:8000`).

### 1. Clone & Install

```bash
git clone https://github.com/your-username/research-agent-ui.git
cd research-agent-ui
npm install
```

### 2. Environment Configuration

Create a `.env.local` file by copying the sample:

```bash
cp .env.local.example .env.local
```

Configure your backend URL in `.env.local`:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api/v1
```

> **Note**: In `next.config.js`, requests to `/api/v1/:path*` are rewritten to `${NEXT_PUBLIC_API_URL}/:path*`. This eliminates browser CORS issues.

### 3. Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to view the application.

---

## 🔌 API & WebSocket Integration

The UI communicates with the backend via REST endpoints and a WebSocket stream:

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/v1/reports` | Queues a new research query (`query`, `max_sources`) |
| `GET` | `/api/v1/reports?limit=10` | Lists recent and active reports |
| `GET` | `/api/v1/reports/:id` | Retrieves full report details and execution state |
| `DELETE` | `/api/v1/reports/:id` | Deletes a report |
| `GET` | `/api/v1/reports/:id/export?format={pdf\|docx}` | Generates and downloads exported documents |
| `WS` | `/api/v1/reports/:id/stream` | Streams live execution logs and progress events |

---

## 📜 Available Scripts

- `npm run dev` - Starts the development server with Hot Module Replacement (HMR).
- `npm run build` - Compiles and optimizes the application for production.
- `npm run start` - Runs the compiled production build.
- `npm run lint` - Runs Next.js ESLint to verify code quality.

---

## 🎨 Theme & Customization

Color tokens are defined in [app/globals.css](file:///c:/Users/SUPRATIM%20NAG/OneDrive/Documents/Github/research-agent-ui/app/globals.css) as CSS custom properties:

```css
:root {
  --ink: #0a0a0f;       /* Background */
  --surface: #13131a;   /* Cards & Panels */
  --border: #1e1e2a;    /* Dividers & Borders */
  --paper: #f5f3ee;     /* Primary Typography */
  --mist: #8a8fa8;      /* Secondary/Muted Text */
  --gold: #c9a84c;      /* Citations & Highlights */
  --accent: #e84234;    /* Primary Action & Badges */
}
```

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
