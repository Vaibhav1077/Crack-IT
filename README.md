# Crack-IT ⚡

**Stop memorizing. Start performing.**

Crack-IT is an AI-powered mock interview platform I built to solve a real problem — most interview prep tools give you a list of questions, but nobody actually *talks* to you, challenges your answers, or tells you why your solution is suboptimal. Crack-IT does all of that.

It simulates a full interview loop: DSA coding rounds, System Design discussions, Resume-based deep dives, and HR behavioral sessions — all driven by AI agents that respond like a real interviewer would.

---

## Why I Built This

I was preparing for placements and realized that solving LeetCode alone wasn't enough. I needed to practice *explaining* my thought process, handling follow-up questions, and performing under pressure. No tool did that well, so I built one.

---

## What It Does

### 🧩 DSA Round
Not just "solve this problem". The interview happens in three phases:
- **Intuition** — explain your approach and complexity before writing any code
- **Coding** — write your solution in a VS Code-style Monaco editor
- **Evaluation** — AI reviews edge cases, complexity, and code quality

### 📄 Resume-Based Round
Upload your PDF resume. The AI reads it and asks questions specifically about your projects, tech stack, and experience — not generic questions pulled from a database.

### 🏗️ System Design Round
High-level architecture discussions. The AI acts as a senior engineer asking you to design scalable systems, pushing back on your decisions and exploring trade-offs.

### 🤝 HR Round
Behavioral questions using the STAR method. Practices culture fit, communication, and situational judgment.

### 📊 Performance Report
After every session, you get a detailed breakdown — what you did well, where you struggled, and what to work on next.

### 🔐 Secure API Key Wallet
You bring your own LLM keys (Groq, Gemini). They are AES-256 encrypted before being stored in the database and only decrypted in-memory during active sessions. Your keys stay yours.

### 🌐 Browser Extension
Extracts questions directly from LeetCode, GeeksForGeeks, Medium, and Reddit so you can practice from real problems without copy-pasting.

---

## Tech Stack

### Frontend
- React 19 + Vite
- Tailwind CSS v4
- Framer Motion (animations)
- Monaco Editor (coding rounds)
- Clerk (authentication)
- Recharts (performance analytics)
- React Webcam (interview simulation environment)

### Backend
- Node.js + Express
- MongoDB + Mongoose
- WebSockets (`ws`) for real-time communication
- LangChain + LangGraph for AI agent orchestration
- Groq API (LLaMA models) — fast inference
- Google Gemini API — multimodal AI
- Judge0 — sandboxed code execution
- pdf-parse — resume parsing

---

## Architecture

```
Client (React) ──── REST API ────► Express Server ──► MongoDB
     │                                    │
     └──── WebSocket ────────────► AI Agent Orchestrator
                                          │
                              ┌───────────┼───────────┐
                         Groq/LLaMA   Gemini API   Judge0
```

### AI Agents

The backend uses a multi-agent system where each agent is a specialist:

| Agent | Role |
|-------|------|
| Interview Plan Agent | Reads resume, generates personalized question plan |
| DSA Agent | Creates coding problems by difficulty |
| DSA Interview Agent | Evaluates code quality, complexity, edge cases |
| System Design Agent | Drives architectural discussions |
| HR Agent | Handles behavioral and situational questions |
| STT Correction Agent | Fixes speech-to-text transcription errors |
| Report Agent | Compiles final performance dashboard |
| Code Generator Agent | Generates test cases and solution scaffolds |

---

## Project Structure

```
Crack-IT/
├── client/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── InterviewSimulation/   # Core interview UI
│   │   │   ├── InterviewRoom/         # Live session room
│   │   │   ├── ResumeUpload/          # Resume upload flow
│   │   │   ├── InterviewHistory/      # Past sessions
│   │   │   └── Report/                # Post-interview analysis
│   │   ├── components/                # Navbar, ProtectedRoute, etc.
│   │   ├── hooks/                     # useInterviewSocket, etc.
│   │   ├── auth/                      # Clerk setup, ApiKeyContext
│   │   └── lib/                       # Gemini live client, audio player
│
├── server/
│   ├── agents/        # All LangChain AI agents
│   ├── graphs/        # LangGraph interview workflows
│   ├── controllers/   # Route handlers
│   ├── models/        # Mongoose schemas
│   ├── routes/        # API endpoints
│   ├── services/      # WebSocket, Judge0, execution logic
│   └── utils/         # Crypto, logging, request context
│
└── extension/         # WXT-based browser extension
    ├── entrypoints/   # Popup, content, background scripts
    ├── extractors/    # Site-specific question extractors
    └── utils/         # API bridge, site detection
```

---

## Getting Started

### 1. Prerequisites
- Node.js v18+
- MongoDB Atlas account (free tier is fine)
- Clerk account (free)
- Groq API key — [console.groq.com](https://console.groq.com) (free)
- Gemini API key — [aistudio.google.com](https://aistudio.google.com) (free)

### 2. Clone & Install

```bash
git clone https://github.com/Vaibhav1077/Crack-IT.git
cd Crack-IT
npm install
cd client && npm install && cd ..
cd server && npm install && cd ..
```

### 3. Environment Setup

```bash
# Server — copy and fill values
cp server/.env.example server/.env

# Client — copy and fill values
cp client/.env.example client/.env
```

**server/.env keys needed:**
```
MONGODB_URI=
CLERK_SECRET_KEY=
CLERK_PUBLISHABLE_KEY=
ENCRYPTION_SECRET=     # 64 hex chars
GEMINI_API_KEY=
GROQ_API_KEY=
JUDGE0_API_KEY=
JUDGE0_API_URL=https://judge0-ce.p.rapidapi.com
```

**client/.env keys needed:**
```
VITE_CLERK_PUBLISHABLE_KEY=
VITE_API_URL=http://localhost:5000
```

### 4. Run

```bash
npm run dev
```

Opens:
- Frontend → http://localhost:5173
- Backend → http://localhost:5000

---

## Roadmap

- [x] DSA, HR, System Design, Resume rounds
- [x] AES-256 encrypted API key wallet
- [x] Real-time WebSocket interview flow
- [x] Browser extension for LeetCode/GFG
- [ ] Multi-language code execution (beyond Python/JS/Java)
- [ ] DSA weak spot heatmap
- [ ] Peer-to-peer mock interview mode
- [ ] Mobile responsive interview UI

---

## License

MIT — use it, fork it, build on it.

---

*Built by Vaibhav — because I needed this tool and it didn't exist.*
