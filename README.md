# Crack-IT ⚡
> **AI-Powered Interview Preparation Platform**

Crack-IT is a full-stack platform that simulates real technical interviews using AI agents. It covers DSA coding rounds, System Design, Resume-based deep dives, and HR behavioral sessions — with real-time feedback, just like a real interviewer.

---

## 🚀 Overview

Unlike static question banks, Crack-IT adapts to your resume, specific job targets, and real-time performance. It uses specialized AI agents and WebSockets for a high-fidelity interview experience.

---

## 🏗️ Architecture

Crack-IT follows a Full-Stack MERN architecture, enhanced with LangChain/LangGraph for AI orchestration and WebSockets for low-latency real-time interactions.

```
Client (React) ──── REST API ────► Express Server ──► MongoDB
     │                                    │
     └──── WebSocket ────────────► AI Agent Orchestrator
                                          │
                              ┌───────────┼───────────┐
                         Groq/LLaMA   Gemini API   Judge0
```

### 🔐 Security — API Key Wallet
One of Crack-IT's core features is the **API Key Wallet**:
- Users provide their own LLM API keys (Gemini, Groq, etc.)
- Keys are **AES-256 encrypted** before being stored in MongoDB
- Keys are only decrypted **in-memory** during an active session using a secure `requestContext` pattern
- Your credentials remain completely private and protected

---

## 💻 Tech Stack

### Frontend
- **React 19** + **Vite** — fast modern frontend
- **Tailwind CSS v4** + **Framer Motion** — styling and animations
- **Monaco Editor** — VS Code-style coding experience for DSA rounds
- **Clerk** — secure authentication and social login
- **Recharts** — performance analytics and charts
- **React Webcam** — simulate the real interview environment

### Backend
- **Node.js** + **Express** — REST API server
- **MongoDB** + **Mongoose** — database and schemas
- **WebSockets (`ws`)** — real-time chat, code, and voice interactions
- **LangChain** + **LangGraph** — AI agent orchestration
- **Groq API** — fast LLaMA model inference
- **Google Gemini API** — multimodal AI capabilities
- **Judge0** — sandboxed code execution
- **pdf-parse** — resume PDF parsing

---

## 🤖 AI Agents

Crack-IT uses a multi-agent system where each agent is a specialist:

| Agent | Role |
|-------|------|
| Interview Plan Agent | Reads your resume and generates a personalized question plan |
| DSA Agent | Creates coding problems by difficulty level |
| DSA Interview Agent | Evaluates code for quality, complexity, and edge cases |
| System Design Agent | Drives high-level architectural discussions |
| HR Agent | Handles behavioral and situational questions |
| STT Correction Agent | Fixes speech-to-text transcription errors using AI |
| Report Agent | Compiles post-interview performance dashboard |
| Code Generator Agent | Generates test cases and solution scaffolds |

---

## 🎯 Interview Rounds

### 1. Resume-Based Round
The system parses your PDF resume and generates questions that drill into your specific projects, technologies, and achievements — not generic questions from a database.

### 2. DSA Specialist Round
A structured three-phase coding interview:
- **Intuition Phase** — explain your approach and time complexity before writing code
- **Coding Phase** — write your solution in Monaco editor with real-time feedback
- **Evaluation Phase** — AI analyzes your solution for edge cases and optimizations

### 3. System Design Round
Architectural challenges with AI acting as a senior engineer — pushing back on your decisions, exploring trade-offs, and discussing scalability.

### 4. HR & Behavioral Round
Simulates standard HR screenings focusing on behavioral questions, past experiences, and future goals using the STAR method.

### 5. Interactive Follow-ups
The AI asks follow-up questions if your answer is vague — mimicking real conversational interview flow.

---

## 📁 Project Structure

```
Crack-IT/
├── client/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── InterviewSimulation/   # Core interview UI
│   │   │   ├── InterviewRoom/         # Live session room
│   │   │   ├── ResumeUpload/          # Resume upload flow
│   │   │   ├── InterviewHistory/      # Past sessions list
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
    ├── extractors/    # LeetCode, GFG, Medium, Reddit extractors
    └── utils/         # API bridge, site detection
```

---

## 🛠️ Getting Started

### Prerequisites
- Node.js v18+
- MongoDB Atlas account (free tier works)
- Clerk account (free) — [clerk.com](https://clerk.com)
- Groq API key (free) — [console.groq.com](https://console.groq.com)
- Gemini API key (free) — [aistudio.google.com](https://aistudio.google.com)

### Installation

```bash
# Clone the repo
git clone https://github.com/Vaibhav1077/Crack-IT.git
cd Crack-IT

# Install all dependencies
npm install
cd client && npm install && cd ..
cd server && npm install && cd ..
```

### Environment Variables

Create `server/.env`:
```
MONGODB_URI=your_mongodb_connection_string
CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key
ENCRYPTION_SECRET=your_64_char_hex_string
GEMINI_API_KEY=your_gemini_api_key
GROQ_API_KEY=your_groq_api_key
JUDGE0_API_KEY=your_rapidapi_key
JUDGE0_API_URL=https://judge0-ce.p.rapidapi.com
```

Create `client/.env`:
```
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
VITE_API_URL=http://localhost:5000
```

### Run

```bash
# Runs both client and server concurrently
npm run dev
```

- Frontend → http://localhost:5173
- Backend → http://localhost:5000

---

## 📈 Roadmap

- [x] DSA, HR, System Design, Resume rounds
- [x] AES-256 encrypted API key wallet
- [x] Real-time WebSocket interview flow
- [x] Browser extension for LeetCode and GFG
- [x] Performance reports and analytics
- [ ] Multi-language code execution support
- [ ] DSA weak spot heatmap
- [ ] Peer-to-peer mock interview mode
- [ ] Mobile responsive interview UI

---

## 📄 License

MIT License — free to use, modify, and distribute.
