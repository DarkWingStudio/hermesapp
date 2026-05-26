# HermesApp

Native Android app for [Hermes Agent](https://github.com/NousResearch/hermes-agent) with local inference. No more Termux hell.



![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)


![Phase](https://img.shields.io/badge/Phase-1%20MVP-orange)

![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)


---

## What This Is

ChatGPT-quality mobile UX for local AI. Your conversations stay on your phone (qwen2.5:7b or whatever model you want), with smart routing to external APIs only for tasks that actually need them (image generation, heavy code analysis).

Currently running Hermes Agent through Termux sucks:
- Android kills it randomly
- Config editing on phone keyboard is pain
- Model switching requires terminal commands
- Not a product normal humans can use

This fixes that.

---

## Status: Phase 1 (In Progress)

**What exists now:**
- [ ] Project structure
- [ ] FastAPI gateway
- [ ] React Native scaffold
- [ ] Chat UI
- [ ] Message streaming
- [ ] Conversation management

**What's coming:**
- Phase 2: Memory & skills visual editor
- Phase 3: Model manager (Ollama + HuggingFace downloads)
- Phase 4: Eliminate Termux dependency (Chaquopy)

See [full roadmap](docs/ROADMAP.md) for details.

---

## Features (When Complete)

- 💬 **Native chat interface** — Streaming responses, markdown rendering, conversation history
- 🔒 **Privacy-first** — Personal data stays local, APIs only for specific tasks
- 📦 **Model manager** — One-tap downloads from Ollama/HuggingFace, storage/RAM calculator
- 🧠 **Memory system** — Visual timeline of learned facts, edit/delete/search
- 🛠️ **Skills hub** — Browse, enable, import custom skills
- 🔌 **MCP integration** — Connect external tools
- 🌓 **OLED dark mode** — True black for battery life
- 🖥️ **Cross-platform** — Android first, desktop (Tauri) later

---

## Architecture
┌─────────────────────────────────────┐
│   React Native (Expo)              │
│   Chat UI + Model/Memory Manager   │
└─────────────────────────────────────┘
↓ HTTP/WebSocket
┌─────────────────────────────────────┐
│   FastAPI Gateway (Python)          │
│   Routing + State Management        │
└─────────────────────────────────────┘
↓
┌──────────────┬──────────────┬────────┐
│ Hermes Agent │ Ollama       │ SQLite │
│ (Python)     │ (Local LLM)  │ (Data) │
└──────────────┴──────────────┴────────┘
**Tech Stack:**
- Frontend: React Native (Expo), TypeScript, Zustand
- Backend: FastAPI, Python 3.11+
- Inference: Ollama (local) + configurable API routing
- Storage: SQLite + local files

---