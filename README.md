# AI Prompt Injection Detector

ML-based security middleware that analyzes user-submitted text for AI threats before it reaches an LLM. Uses an **intent-aware 5-phase pipeline**: normalization → intent classification → categorized regex detection → composite risk scoring → response policy.

## Features

- FastAPI API: `/analyze`, `/health`, `/logs`, `/analytics`, `/red-team/*`
- 12-category threat detection with intent-aware scoring
- TF-IDF + Logistic Regression ML classifier
- Red-team LLM proxy endpoints (Anthropic key stays server-side)
- Optional **SecureChat** UI in `chatbot/` (FastAPI + static frontend)

## Quick start (local)

```bash
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

```bash
curl http://localhost:8000/health
curl -X POST http://localhost:8000/analyze \
  -H "Content-Type: application/json" \
  -d '{"text": "hello", "source": "test"}'
```

## Deploy on Render

1. [Connect this repo on Render](https://render.com/deploy)
2. Render reads `render.yaml` and creates **prompt-injection-detector**
3. Set **ANTHROPIC_API_KEY** and **RED_TEAM_API_KEY** in Environment
4. Copy the live URL for the red-team repo's `DETECTOR_URL`

## Optional: SecureChat UI

```bash
cd chatbot
cp .env.example .env   # set ANTHROPIC_API_KEY, DETECTOR_URL
pip install -r requirements.txt
python web_server.py   # http://localhost:3000
```

Deploy `chatbot/` separately on Vercel (see `chatbot/README.md`).

## Tests

```bash
python -m pytest tests/ -v
```

## Related repo

- [prompt-injection-red-team](https://github.com/sunehrisahel/prompt-injection-red-team) — Streamlit adversarial evaluation console

## License

MIT
