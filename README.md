<div align="center">

<img src="https://img.shields.io/badge/LocalMind-v2.0.0-7C3AED?style=for-the-badge&logoColor=white" />

# 🧠 LocalMind v2.0
### Offline AI Assistant — Chat with Your Documents. Privately.

**No cloud. No API key. No data leaks. Runs 100% on your machine.**

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=flat-square&logo=fastapi)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev)
[![Ollama](https://img.shields.io/badge/Ollama-Local_LLM-black?style=flat-square)](https://ollama.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![SSoC 2026](https://img.shields.io/badge/SSoC-2026-blueviolet?style=flat-square)](https://ssoc.dev)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)](CONTRIBUTING.md)

<br/>

[🚀 Quick Start](#-quick-start) · [✨ Features](#-features) · [🛠 Tech Stack](#-tech-stack) · [🤝 Contributing](#-contributing) · [📸 Screenshots](#-screenshots)

---

</div>

## ✨ What's New in v2.0

| Feature | Description |
|---------|-------------|
| ⚡ **Streaming Responses** | See AI reply token-by-token in real time |
| 🔌 **Plugin System** | Calculator, Word Counter, JSON Formatter, Code Runner, Summarizer |
| 🌐 **8 Languages** | English, Hindi, Tamil, Telugu, Kannada, French, German, Spanish |
| 📤 **Export Chats** | Download conversations as Markdown, JSON, or TXT |
| 🗂 **Session Manager** | Full CRUD — create, rename, search, delete chat sessions |
| ⚙️ **Settings Panel** | Temperature, RAG chunks, model, theme, language |
| 🐳 **Docker v2** | Health checks, persistent volumes, nginx reverse proxy |
| 🧪 **30+ Tests** | Full pytest suite with mocked Ollama |

---

## ✨ All Features

| Feature | Status |
|---------|--------|
| 🏠 Fully Offline (Ollama) | ✅ |
| 📄 PDF / TXT / CSV / DOCX / MD / HTML upload | ✅ |
| 🧠 RAG — Chat with Documents | ✅ |
| ⚡ Streaming Responses (SSE) | ✅ |
| 🤖 Multi-Model (Llama3, Mistral, Phi3, Gemma, DeepSeek) | ✅ |
| 🌐 8 UI Languages | ✅ |
| 💬 Chat History (SQLite) | ✅ |
| 🗂 Session Manager (CRUD) | ✅ |
| 🔍 Session Search | ✅ |
| 🔌 Plugin System (6 plugins) | ✅ |
| 📤 Export (MD / JSON / TXT) | ✅ |
| ⚙️ Settings Panel | ✅ |
| 🐳 Docker Compose | ✅ |
| 🧪 30+ Tests | ✅ |
| 🔒 Zero telemetry | ✅ |

---

## 🛠 Tech Stack

```
┌────────────────────────────────────────────────┐
│               LocalMind v2.0                   │
├──────────────┬─────────────────────────────────┤
│  Frontend    │  React 18 + Tailwind + Vite      │
│  Backend     │  Python 3.11 + FastAPI           │
│  AI Engine   │  Ollama (local LLM)              │
│  RAG         │  LangChain + ChromaDB            │
│  Embeddings  │  sentence-transformers (local)   │
│  Database    │  SQLite (100% local)             │
│  Streaming   │  Server-Sent Events (SSE)        │
│  Deploy      │  Docker Compose + nginx          │
│  Testing     │  pytest + TestClient             │
└──────────────┴─────────────────────────────────┘
```

---

## 🚀 Quick Start

### Option 1 — Docker (Recommended, 3 commands)

```bash
# 1. Pull a model (one-time, ~4GB)
ollama pull llama3

# 2. Clone and start
git clone https://github.com/yourusername/localmind.git
cd localmind && docker compose up

# 3. Open browser
open http://localhost:3000
```

### Option 2 — Manual Setup

```bash
git clone https://github.com/yourusername/localmind.git
cd localmind

# Backend
cd backend
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp ../.env.example ../.env
uvicorn app:app --reload --port 8000

# Frontend (new terminal)
cd frontend
npm install && npm run dev
# Open http://localhost:3000
```

**Prerequisites:** [Python 3.11+](https://python.org) | [Node 18+](https://nodejs.org) | [Ollama](https://ollama.ai) | [Docker](https://docker.com)

---

## 📁 Project Structure

```
localmind/
├── backend/
│   ├── app.py                    # FastAPI entry point
│   ├── routes/
│   │   ├── chat.py               # /api/chat — streaming + standard
│   │   ├── sessions.py           # /api/sessions — full CRUD
│   │   ├── upload.py             # /api/upload — file indexing
│   │   ├── models.py             # /api/models — Ollama management
│   │   ├── plugins.py            # /api/plugins — 6 built-in plugins
│   │   ├── export.py             # /api/export — MD, JSON, TXT
│   │   └── settings.py           # /api/settings — app config
│   ├── services/
│   │   ├── rag_service.py        # LangChain + ChromaDB RAG
│   │   ├── ollama_service.py     # Ollama + streaming
│   │   └── db_service.py        # SQLite — all CRUD
│   ├── models/
│   │   └── schemas.py           # Pydantic v2 schemas
│   ├── tests/
│   │   └── test_api.py          # 30+ tests
│   ├── requirements.txt
│   └── Dockerfile
├── frontend/
│   ├── src/
│   │   ├── App.jsx               # Root — state, routing
│   │   ├── components/
│   │   │   ├── ChatWindow.jsx    # Messages + streaming + export
│   │   │   ├── Sidebar.jsx       # Sessions + model + language
│   │   │   ├── StatusBar.jsx     # Header toolbar
│   │   │   ├── UploadPanel.jsx   # Drag-drop file upload
│   │   │   ├── PluginsPanel.jsx  # Plugin runner UI
│   │   │   └── SettingsPanel.jsx # Settings form
│   │   └── utils/
│   │       └── api.js            # All backend API calls
│   ├── package.json
│   ├── vite.config.js
│   └── Dockerfile
├── docker-compose.yml
├── .env.example
├── .gitignore
├── README.md
├── CONTRIBUTING.md
└── ROADMAP.md
```

---

## 🔌 Plugins

| Plugin | Description |
|--------|-------------|
| 🧮 Calculator | Safe math evaluator (supports `sqrt`, `log`, `sin`, etc.) |
| 📝 Summarizer | Extractive summary of long text |
| 🔢 Word Counter | Words, chars, sentences, paragraphs |
| {} JSON Formatter | Validate and pretty-print JSON |
| ⚡ Code Runner | Run Python snippets in a sandbox |
| 🌐 Translator | Language detection + translation via LocalMind |

---

## 🧪 Running Tests

```bash
cd backend
pip install pytest pytest-asyncio
pytest tests/ -v
# 30+ tests covering: sessions, chat, plugins, upload, export, settings
```

---

## 🤝 Contributing

1. Fork → Clone → Create branch (`git checkout -b feature/your-feature`)
2. Make changes → Write tests → Commit (`git commit -m "feat: ..."`)
3. Push → Open Pull Request

Issues labeled [`good-first-issue`](https://github.com/yourusername/localmind/issues?q=label%3Agood-first-issue) are perfect for beginners!

Read [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide.

---

## 📄 License

MIT © 2026 — Made with ❤️ for [Social Summer of Code 2026](https://ssoc.dev)

<div align="center">

⭐ **If LocalMind helped you, please star the repo!** ⭐

</div>