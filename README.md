<div align="center">

# 🧠 Medmind-AI

### AI-powered medical assistant for clinicians — triage, summarization, and lightweight model tooling  
**Privacy-first • Research-friendly • Ready for prototyping**

[![Stars](https://img.shields.io/github/stars/DhanushGroot/Medmind-AI?style=for-the-badge&logo=github)](https://github.com/DhanushGroot/Medmind-AI/stargazers)
[![Version](https://img.shields.io/badge/version-0.1.0-blue?style=for-the-badge)](./)
[![Build](https://img.shields.io/badge/build-passing-brightgreen?style=for-the-badge)](https://github.com/DhanushGroot/Medmind-AI/actions)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

</div>

---

## ✨ Demo / Preview

<div align="center">

**Try the demo UI or run locally**

![Medmind Preview](/assets/demo.gif)

</div>

---

## 🚀 What Medmind-AI Delivers

- Rapid clinical note summarization (concise, structured outputs)  
- Symptom triage assistance & risk flags for prioritization  
- Modular model backends (local or remote) so you keep data private  
- Upload + annotate patient notes, export summaries and reports  
- Notebook-first UX for reproducible experiments

---

## 🔑 Features

- 📝 Clinical note summarization (transformer-based or lightweight alternatives)  
- ⚖️ Token-limited safe outputs with hallucination guards  
- 🔌 Pluggable model wrappers (Hugging Face, local checkpoints, remote APIs)  
- 📂 Upload & batch processing for document-level inference  
- 📑 Export summaries as JSON, TXT or PDF for downstream workflows  
- 🧪 Notebooks for evaluation, benchmarks, and examples

---

## 🛠️ Tech Stack

| Layer | Technology |
|------:|:-----------|
| Frontend | HTML, CSS, minimal JS (static UI) |
| Backend | Python (FastAPI / Flask compatible) |
| ML | Hugging Face Transformers, spaCy (NER), scikit-learn utilities |
| Data | Local JSON / SQLite for demo persistence |
| Dev | pip, venv, Docker (optional) |

---

## ⚙️ Architecture — How it Works

```
Medmind-AI
├── frontend/                → static UI (index.html, assets)
├── backend/
│   ├── app.py               → FastAPI / Flask endpoints
│   ├── api/
│   │   └── summarize.py     → model pipeline wrapper
│   └── models/
│       └── hf_wrapper.py    → HuggingFace / local model adapters
├── notebooks/               → reproducible demos & evals (.ipynb)
├── assets/                  → demo.gif, sample notes
└── docker/                  → optional Docker configs
```

Data flow — user uploads note → frontend POST /api/summarize → backend pipeline (preprocess → model → postprocess) → structured summary → frontend / export

<details>
<summary>🔎 Component responsibilities</summary>

- frontend/index.html — upload UI, settings, export buttons  
- backend/app.py — REST surface (POST /api/summarize, GET /health)  
- backend/api/summarize.py — orchestrates tokenization, inference, safety checks, output formatting  
- backend/models/hf_wrapper.py — lightweight adapter for HF pipelines or local checkpoints  
- notebooks/ — examples for benchmarking, NER extraction, and evaluation metrics

</details>

---

## 📦 Installation

Pick local Python environment or Docker.

### Local (venv recommended)

```bash
# Clone
git clone https://github.com/DhanushGroot/Medmind-AI.git
cd Medmind-AI

# Create venv and install
python -m venv .venv
source .venv/bin/activate
pip install -r backend/requirements.txt

# Run the API
uvicorn backend.app:app --reload --host 0.0.0.0 --port 8000

# Open frontend/index.html and point to http://localhost:8000
```

### Docker

```bash
# Build & run (if Dockerfile present)
docker build -t medmind-ai .
docker run -p 8000:8000 medmind-ai
```

---

## 💻 Usage Examples

### Summarize a note (curl)
```bash
curl -X POST http://localhost:8000/api/summarize \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Patient is a 58-year-old male with chest pain and shortness of breath...",
    "model": "local-distilbart",
    "max_tokens": 150
  }'
```

### Minimal FastAPI endpoint (illustrative)
```python
# backend/app.py (excerpt)
from fastapi import FastAPI
from api.summarize import summarize_text

app = FastAPI()

@app.post("/api/summarize")
async def summarize(payload: dict):
    summary = await summarize_text(payload["text"], model=payload.get("model"))
    return {"summary": summary}
```

### Notebook example (quick)
Open notebooks/demo_summarization.ipynb to run model evaluations and view example outputs.

---

## 🧭 Configuration

- backend/config.py — model selection, tokenizer settings, safety thresholds  
- Use local checkpoints or set HF_API_KEY to call remote endpoints  
- Keep PHI/PII in mind: prefer local models for sensitive data

Example config excerpt:
```python
MODEL_BACKENDS = {
  "local-distilbart": {"path": "checkpoints/distilbart"},
  "hf-remote": {"api_key_env": "HF_API_KEY", "endpoint": "https://api.hf.example/v1"}
}
SAFETY = {"max_tokens": 200, "allow_list": [], "deny_list": ["diagnose without clinician"]}
```

---

## 🗺️ Roadmap

- [x] Core summarization endpoint & demo UI  
- [x] Notebook examples + evaluation scripts  
- [ ] Clinical NER extraction & structured field output  
- [ ] Offline-only model bundles for on-premise use  
- [ ] Benchmarks & model comparison dashboard  
- [ ] Authentication & audit logging for clinical deployments

---

## 🤝 Contributing

Contributions welcome — prefer small, focused PRs with notebooks or tests.

1. Fork the repo  
2. Create a branch: git checkout -b feat/your-feature  
3. Add tests/notebooks demonstrating behavior  
4. Open a PR describing expected outputs and performance

Please avoid committing large model weights to the repo; use checkpoints or HF references.

---

## 📈 Live Metrics

<div align="center">

![Repo Stats](https://github-readme-stats.vercel.app/api?username=DhanushGroot&repo=Medmind-AI&show_icons=true&theme=dark&hide_border=true)
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=DhanushGroot&repo=Medmind-AI&layout=compact&theme=dark&hide_border=true)

<br />

![GitHub Streak](https://github-readme-streak-stats.herokuapp.com/?user=DhanushGroot&theme=dark&hide_border=true)
![Profile Views](https://komarev.com/ghpvc/?username=DhanushGroot&color=49c5b6)

</div>

---

## 📝 License

MIT — see LICENSE.

---

Made for fast prototyping and careful evaluation — Medmind-AI © DhanushGroot  
*Last updated: 2026-04-22*
