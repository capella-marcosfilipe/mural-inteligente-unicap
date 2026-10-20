# Mural Inteligente UNICAP — Smart Bulletin Board

**Full-stack + AI workshop** taught at the UNICAP Technology Journey 2026 by the FASA/UNICAP AI Center.

Take a photo of a printed notice from a campus bulletin board → a computer-vision model describes it → an LLM agent decides whether it is relevant and extracts structured information → an Angular dashboard shows it in real time.

## AI pipeline (LangGraph)

```text
[Photo of the notice]
        │
        ▼
   VisionNode        BLIP generates a text description of the image
        │
        ▼
  ReasoningNode      Groq LLM classifies relevance and structures the data
        │
        ▼
  data/data.json     Structured notice is persisted
        │
        ▼
 Angular dashboard   Real-time display with Signals
```

The shared graph state (`AgentState`) carries `image_path`, `raw_description`, `is_relevant`, `structured_data` and `history`.

## Stack

| Layer | Tech |
|---|---|
| Backend | Python, FastAPI, Uvicorn, Pydantic Settings |
| AI | LangGraph, LangChain-Groq, Hugging Face Transformers (BLIP), PyTorch (CPU), Pillow |
| Frontend | Angular 21 (standalone components), TypeScript 5.9, RxJS, Signals |

## Running

Requirements: Python 3.11+, Node.js 20+ / npm 11+, and a free Groq API key from [console.groq.com](https://console.groq.com).

### Backend

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r backend/requirement.txt

cp backend/.env.example backend/.env   # then set GROQ_API_KEY
uvicorn backend.main:app --reload      # http://localhost:8000
```

### Frontend

```bash
cd frontend
npm install
npm start                              # http://localhost:4200
```

## Author

**Marcos Filipe Capella** — Jr. AI Software Engineer, FASA/UNICAP AI Center · [LinkedIn](https://www.linkedin.com/in/capella-marcosfilipe) · [marcoscapella.com.br](https://marcoscapella.com.br)
