<div align="center">
  <img src="assets/images/logo_entrevistat.png" alt="Entrevista't logo" width="200" height="auto" />
  <h1>Entrevista't</h1>

  <p>
    Plataforma de preparació d'entrevistes amb IA
  </p>

  <p>
    <img src="https://img.shields.io/badge/Flutter-3.27.1-02569B?logo=flutter" alt="Flutter" />
    <img src="https://img.shields.io/badge/FastAPI-0.115-009688?logo=fastapi" alt="FastAPI" />
    <img src="https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white" alt="Python" />
    <img src="https://img.shields.io/badge/PostgreSQL-336791?logo=postgresql&logoColor=white" alt="PostgreSQL" />
    <img src="https://img.shields.io/badge/Docker-ready-2496ED?logo=docker" alt="Docker" />
    <img src="https://img.shields.io/badge/Language-Català-FFCD00" alt="Catalan" />
  </p>
</div>

<br />

---

## About

**Entrevista't** is an AI-powered interview practice platform built as an academic project. Users pick a job category, answer timed questions on camera, and receive automated feedback with scores across audio, text, and emotional dimensions — plus a downloadable PDF report.

All user-facing text is in **Catalan (Català)**. Code, comments, and documentation are in English.

### How It Works

```
Pick a category → Answer questions on camera → AI analyses your performance
  → Get scores, charts, and a PDF report
```

The platform evaluates candidates across three dimensions:

- 🎙️ **Audio** — speech duration, pause patterns, communication rhythm (WPM)
- 📝 **Text** — question alignment, coherence, information density, lexical richness, confidence index (7 NLP metrics)
- 😊 **Video** — emotion distribution, dominant emotion, emotional stability via face analysis

---

## Repositories

| Repository | Description | Stack |
|------------|-------------|-------|
| [**Front**](https://github.com/Entrevista-t/Front) | Web & mobile client — camera capture, results dashboard, PDF reports | Flutter 3.27 · Dart · GoRouter · Docker |
| [**Back**](https://github.com/Entrevista-t/Back) | API server & AI analysis pipeline — transcription, NLP, emotion detection | FastAPI · Python 3.12 · Whisper · spaCy · DeepFace · PostgreSQL |

---

## Architecture Overview

```
┌─────────────────────────────────┐         ┌─────────────────────────────────┐
│           Frontend              │         │            Backend              │
│                                 │         │                                 │
│  Flutter (Web & Mobile)         │         │  FastAPI + PostgreSQL           │
│                                 │  HTTP   │                                 │
│  Camera capture ────────────────┼────────►│  /analyze ──► AI Pipeline       │
│  Auth (JWT) ────────────────────┼────────►│  /auth/*  ──► bcrypt + JWT      │
│  Results & charts ◄─────────────┼────────┤  /health, /test-db              │
│                                 │         │                                 │
│  Glassmorphism UI               │         │  ┌───────────────────────────┐  │
│  Light & dark themes            │         │  │  interview_analyzer/      │  │
│  Responsive (desktop + mobile)  │         │  │  ├─ audio.py (librosa)    │  │
│                                 │         │  │  ├─ transcription.py      │  │
│                                 │         │  │  │  (Whisper)             │  │
│                                 │         │  │  ├─ text.py (spaCy +     │  │
│                                 │         │  │  │  SentenceTransformers) │  │
│                                 │         │  │  ├─ video.py (DeepFace + │  │
│                                 │         │  │  │  MediaPipe)            │  │
│                                 │         │  │  └─ pipeline.py          │  │
│                                 │         │  └───────────────────────────┘  │
└─────────────────────────────────┘         └─────────────────────────────────┘
```

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | Flutter 3.27 · Dart 3.6 · GoRouter · fl_chart · camera plugin |
| **Backend** | FastAPI · Uvicorn · Pydantic · SQLAlchemy 2.0 |
| **Database** | PostgreSQL (JSONB for metrics) |
| **Auth** | JWT (PyJWT) · bcrypt (passlib) |
| **AI — Audio** | OpenAI Whisper · librosa · ffmpeg |
| **AI — NLP** | spaCy (`ca_core_news_md`) · SentenceTransformers · scikit-learn |
| **AI — Vision** | MediaPipe FaceMesh · DeepFace |
| **Infra** | Docker · GitHub Actions · Docker Swarm · GHCR |

---

## Getting Started

Both repositories include interactive launcher scripts (`start.ps1` / `start.sh`) and Docker Compose setups. See each repo's README for detailed instructions.

### Quick Start

```bash
# 1. Clone both repos
git clone https://github.com/Entrevista-t/Back.git
git clone https://github.com/Entrevista-t/Front.git

# 2. Start the backend (http://localhost:8000)
cd Back
cp .env.example .env          # Configure DATABASE_URL
./start.ps1                    # Option 1: Start dev server

# 3. Start the frontend (http://localhost:8080)
cd ../Front
./start.ps1                    # Option 1: Start dev server
```

---

## Disclaimer

This project is under active development as part of an academic initiative. Features and APIs may change without notice.

---

## License

No formal license has been declared yet. Please contact the maintainers for usage permissions.
