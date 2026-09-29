# HackInteliX: Evidence-Grounded AI-Powered Hackathon Management Platform

> **Final-Year Computer Engineering / Research Project**  
> *"Node.js manages the application platform; Python provides a specialized AI/ML service for 384-dim sentence embeddings, hybrid RAG retrieval, NLP, and explainable ML analytics. AI assists the judge; human judges retain final authority."*

HackInteliX converts the complete software-development journey of a hackathon team into structured, verifiable evidence for human judges. Instead of judging only the final presentation, HackInteliX collects evidence across commits, AST code symbols, security SAST findings, container test execution, peer code reviews, and 384-dimensional dense semantic vector retrieval.

---

## 🏛️ System Architecture

```
                    HACKINTELIX
                         │
                         ▼
              React + Vite Frontend
                         │
                         ▼
              Node.js + Express
                         │
        ┌────────────────┼──────────────────┐
        │                │                  │
        ▼                ▼                  ▼
     MongoDB         GitHub APIs        Webhooks
        │
        │
        ├───────────────┐
        │               │
        ▼               ▼
 Evidence/Data     MongoDB Vector Search
                        ▲
                        │
                 Python FastAPI
                        │
       ┌────────────────┼──────────────────┐
       │                │                  │
       ▼                ▼                  ▼
 Real 384-dim Embeddings  RAG            ML/NLP
       │                │                  │
       │          ┌─────┴─────┐            │
       │          │           │            │
       │        BM25       Vector Search   │
       │          │           │            │
       │          └─────┬─────┘            │
       │                ▼                  │
       │            Reranking              │
       │                │                  │
       └────────────────┼──────────────────┘
                        ▼
                       LLM
                        │
                        ▼
               Evidence-Grounded AI
                        │
             ┌──────────┼──────────┐
             ▼          ▼          ▼
        Repository   Contribution  Judge
        Intelligence  Analytics    Assistant
                        │
                        ▼
                  Human Judge
                        │
                        ▼
                 Final Evaluation
```

---

## 🚀 Key Architectural Features

- **Decoupled Hybrid Architecture:**
  - **Node.js / Express:** Primary application backend responsible for JWT Auth, RBAC, User Management, Organizations, Hackathons, Teams, Submissions, Evaluations, GitHub OAuth & Webhooks, MongoDB operations, and Container Sandbox orchestration.
  - **Python / FastAPI (`ai-service`):** Specialized microservice handling 384-dimensional pretrained sentence embeddings (`sentence-transformers/all-MiniLM-L6-v2`), BM25 keyword search + 384-dim dense vector fusion, score reranking, provider-independent LLM service, AST/code similarity, and explainable ML analytics.
- **Real Pretrained 384-dim Vector Embeddings:** Uses `sentence-transformers/all-MiniLM-L6-v2` to generate genuine semantic representations stored in MongoDB Vector Search.
- **Hybrid Retrieval Engine (BM25 + 384-dim Dense Vectors):** Exact keyword BM25 scoring fused with dense vector cosine similarity using configurable `BM25_WEIGHT=0.5` and `VECTOR_WEIGHT=0.5`.
- **Anti-Hallucination Guardrails:** If retrieved evidence score is below threshold, outputs `"Insufficient evidence found in the repository to answer this query."`
- **Explainable ML Analytics:** Python `ml` module uses `numpy`, `pandas`, and `scikit-learn` IsolationForest for contribution anomaly detection, graph network collaboration analysis, and weighted repository health scoring, clearly labeled as *"Observed contribution activity"*.
- **AI Judge Assistant with Citations:** Generates rubric recommendations with source code line citations. Final evaluation scores remain under 100% human judge control.

---

## 🛠️ Technology Stack

| Component | Technology |
|---|---|
| **Frontend** | React, Vite, JavaScript, Tailwind CSS, Lucide Icons, Recharts |
| **App Backend** | Node.js, Express, JavaScript (Auth, RBAC, GitHub Sync, Sandboxes) |
| **AI/ML Service** | Python 3.11+, FastAPI, PyTorch, Sentence-Transformers, NumPy, Pandas, Scikit-learn |
| **Database** | MongoDB, Mongoose, MongoDB Vector Search |
| **Embeddings** | `sentence-transformers/all-MiniLM-L6-v2` (384-dimensional dense vectors) |
| **Retrieval** | BM25 Keyword Search + Dense Vector Cosine Similarity Fusion + Reranking |
| **Infrastructure** | Docker, Docker Compose, GitHub Actions CI/CD |

---

## ⚡ Quick Start & Setup

### 1. Install Node & Python Dependencies
```bash
# Node backend
cd backend && npm install

# Frontend
cd ../frontend && npm install

# Python AI Service
cd ../ai-service && pip install -r requirements.txt
```

### 2. Configure Environment Variables
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```

### 3. Run Microservices
```bash
# Terminal 1: Python AI Microservice (Port 8000)
cd ai-service && python main.py

# Terminal 2: Node Application Backend (Port 5000)
cd backend && npm start

# Terminal 3: React Frontend (Port 5173)
cd frontend && npm run dev
```

### 4. Run via Docker Compose
```bash
docker-compose up --build
```

---

## 🧪 Testing

```bash
# Run Python AI Service tests
python ai-service/tests/run_tests.py

# Run Node Backend integration tests
cd backend && npm test

# Build Frontend production bundle
cd frontend && npm run build
```
