
# HermesApp

Native Android app for [Hermes Agent](https://github.com/NousResearch/hermes-agent) with local inference. No more Termux hell.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Phase](https://img.shields.io/badge/Phase-1%20MVP-orange)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)]()

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

```
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
```

**Tech Stack:**
- Frontend: React Native (Expo), TypeScript, Zustand
- Backend: FastAPI, Python 3.11+
- Inference: Ollama (local) + configurable API routing
- Storage: SQLite + local files

---

## Quick Start

> ⚠️ **Phase 1 is incomplete.** These instructions will work once MVP is ready.

### Prerequisites
- Android phone with 8GB+ RAM
- Termux installed
- Hermes Agent installed in Termux ([guide](https://github.com/NousResearch/hermes-agent))
- Node.js 18+ (for development)

### Installation

**1. Clone and setup gateway:**
```bash
cd gateway
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python main.py  # Starts on localhost:8765
```

**2. Run mobile app:**
```bash
cd mobile
npm install
npm start
# Scan QR code with Expo Go app
```

**3. Connect to gateway:**
Open app → Settings → Enter gateway URL: `http://YOUR_PHONE_IP:8765`

---

## Development

See [CONTRIBUTING.md](CONTRIBUTING.md) for development setup.

**Project structure:**
```
hermesapp/
├── mobile/          # React Native app
├── gateway/         # FastAPI backend
├── desktop/         # Tauri desktop app (Phase 4)
├── docs/            # Documentation
└── scripts/         # Setup/deployment scripts
```

**Run tests:**
```bash
# Gateway
cd gateway && pytest

# Mobile
cd mobile && npm test
```

---

## Why This Exists

Hermes Agent is incredible but Termux UX is terrible for daily use. This makes it actually usable for non-terminal people while keeping the privacy benefits of local inference.

**Design goals:**
1. Zero compromise on UX (match ChatGPT mobile app quality)
2. Privacy by default (local first, APIs optional)
3. No vendor lock-in (swap models/APIs anytime)
4. Actually maintainable (clean architecture, not a hackathon project)

---

## Roadmap

### Phase 1: MVP (6-8 weeks) ← Current
- Native chat UI with streaming
- Conversation management
- Basic settings
- Model switching

### Phase 2: Memory & Skills (4 weeks)
- Visual memory timeline
- Skills manager
- MCP integration

### Phase 3: Model Manager (4 weeks)
- Browse Ollama library
- One-tap downloads
- HuggingFace integration
- Storage management

### Phase 4: Production (6 weeks)
- Eliminate Termux (Chaquopy)
- Desktop version (Tauri)
- Beta testing

**Total timeline: ~5 months to v1.0**

See [detailed PRD](docs/PRD.md) for full specs.

---

## Contributing

This is early. Here's how you can help:

**Right now:**
- Try the architecture and tell me if it's stupid
- Review the [PRD](docs/PRD.md) and suggest changes
- Open issues for must-have features I'm missing

**Soon (once Phase 1 works):**
- Fix bugs
- Add features
- Improve UI/UX
- Write tests

**Guidelines:**
- Read [CONTRIBUTING.md](CONTRIBUTING.md) first
- Open an issue before big PRs
- Keep PRs small and focused
- Write tests for new features

---

## FAQ

**Q: Why not just use ChatGPT/Claude mobile apps?**  
A: Your data goes to their servers. This keeps everything local.

**Q: Why not just use Termux?**  
A: Try editing JSON configs on a phone keyboard. Also Android kills Termux constantly.

**Q: React Native or Flutter?**  
A: React Native for now. Might port to Flutter if performance sucks.

**Q: Will this work on iOS?**  
A: No. Ollama doesn't run on iOS. This is Android + Desktop only.

**Q: When can I install this?**  
A: Phase 1 MVP in ~6-8 weeks. Follow for updates.

**Q: Can I use my own API keys (OpenAI, Anthropic, etc.)?**  
A: Yes (Phase 3). The whole point is routing: local for personal stuff, APIs for heavy tasks.

**Q: Is this affiliated with Nous Research?**  
A: No, just a wrapper around their excellent Hermes Agent.

---

## License

MIT - see [LICENSE](LICENSE)

Built on top of [Hermes Agent](https://github.com/NousResearch/hermes-agent) by Nous Research.

---

## Status Updates

Follow development:
- 📦 **Reddit:** [r/androiddev](https://reddit.com/r/androiddev) (will post updates)
- 💬 **Issues:** [GitHub Issues](https://github.com/DarkWingstudio/hermesapp/issues)
- 📋 **Project Board:** [Coming soon]

---

## Acknowledgments

- [Hermes Agent](https://github.com/NousResearch/hermes-agent) - The AI agent this wraps
- [Ollama](https://ollama.ai) - Local inference engine
- Everyone who gave feedback on the [initial Reddit post](LINK_WHEN_POSTED)

---

**Current status:** Planning → Building → Testing → Shipping

Star this repo if you want local AI that doesn't suck on mobile. 🚀
```

---

## Additional Files to Create

**CONTRIBUTING.md** (basic version):
```markdown
# Contributing

This project is in early development. Here's how to help:

## Development Setup

1. **Prerequisites:**
   - Node.js 18+
   - Python 3.11+
   - Android Studio (for emulator)
   - Hermes Agent installed

2. **Clone and install:**
   ```bash
   git clone https://github.com/DarkWingstudio/hermesapp
   cd hermesapp
   
   # Gateway
   cd gateway && pip install -r requirements.txt
   
   # Mobile
   cd mobile && npm install
   ```

3. **Run locally:**
   - Terminal 1: `cd gateway && python main.py`
   - Terminal 2: `cd mobile && npm start`

## Guidelines

- Open an issue before big features
- Keep PRs focused (one feature/fix per PR)
- Write tests for new code
- Follow existing code style
- Be nice

## Questions?

Open an issue or DM me on Reddit: DarkWingStudio


---

Ship this README as your first commit. Update it as you build. Don't wait for perfection.