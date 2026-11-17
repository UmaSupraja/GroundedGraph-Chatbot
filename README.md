# GroundedGraph-Chatbot

### [View the live GroundedGraph-Chatbot](https://langgraph-pinecone-rag-chatbot.onrender.com/)

> The free Render tier can sleep when idle, so the first load may take up to a minute.

GroundedGraph-Chatbot is a Retrieval-Augmented Generation (RAG) chatbot built with **Google Gemini**, **Pinecone**, **LangGraph**, **React**, **TypeScript** and **Express**.

It answers questions from the *Agentic AI for Executives* eBook. Every answer is checked for relevance, scope and groundedness, and comes with page-level source references. Questions the eBook cannot answer are declined instead of guessed.

---

## Features

- Retrieval-Augmented Generation over a Pinecone vector index
- Gemini embeddings and Gemini-powered response generation
- LangGraph workflow orchestration
- Document relevance grading
- Question scope validation (out-of-scope questions are declined)
- Groundedness validation of generated answers
- Source page references with every answer
- React + TypeScript chat interface
- Express backend API
- Production deployment on Render
- Python LangGraph + FastAPI reference implementation

---

## System Architecture

```
                    User
                     │
                     ▼
          React + TypeScript UI
                     │
                     ▼
             Express Backend
                     │
                     ▼
          LangGraph RAG Workflow
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
   Query Processing        Pinecone Search
                                │
                                ▼
                       Relevant Documents
                                │
                                ▼
                       Relevance Grading
                                │
                                ▼
                         Scope Validation
                                │
                                ▼
                       Gemini Generation
                                │
                                ▼
                      Groundedness Check
                                │
                                ▼
                         Final Response
                                │
                                ▼
                       Answer + Sources
```

---

## Project Structure

```
GroundedGraph-Chatbot/
├── src/
│   ├── components/
│   │   └── ChatWorkbench.tsx
│   └── data/
│       └── ebook_pages.ts
├── server/
│   ├── rag_workflow.ts
│   └── pinecone_service.ts
├── python_submission/
│   └── Python LangGraph + FastAPI implementation
├── server.ts
├── package.json
├── vite.config.ts
├── .env.example
├── .gitignore
└── README.md
```

---

## Technologies Used

| Technology    | Purpose                               |
| ------------- | ------------------------------------- |
| React         | Frontend user interface               |
| TypeScript    | Application development               |
| Vite          | Frontend dev server and build tool    |
| Express       | Backend API server                    |
| LangGraph     | RAG workflow orchestration            |
| Google Gemini | Embeddings and response generation    |
| Pinecone      | Vector database and similarity search |
| Python        | Reference RAG implementation          |
| FastAPI       | Python API                            |
| dotenv        | Environment variable management       |

---

## Knowledge Base

The chatbot is grounded in the eBook **Agentic AI for Executives**. Page-level content is stored and retrieved through vector search.

| Setting         | Value                         |
| --------------- | ----------------------------- |
| Pinecone index  | `agentic-ai-rag`              |
| Embedding model | `gemini-embedding-2-preview`  |
| Vector dimension| `3072`                        |

> `gemini-embedding-2-preview` is a preview model and may change or be retired. If you switch models, re-ingest the eBook and recreate the Pinecone index with the matching dimension.

---

## How It Works

1. **User question:** submitted through the React interface.
2. **Query processing:** the backend passes the question into the LangGraph workflow.
3. **Vector retrieval:** the query is embedded and matched against Pinecone.
4. **Document grading:** retrieved chunks are scored for relevance.
5. **Scope validation:** the workflow checks whether the eBook can answer the question.
6. **Response generation:** Gemini answers using only the retrieved context.
7. **Groundedness validation:** the answer is checked against that context.
8. **Final response:** the answer is returned with source page references.

### Scope control example

```
Question: What is the capital of France?
Result:   The question is outside the scope of the available knowledge base.
```

---

## Installation

```bash
git clone https://github.com/UmaSupraja/GroundedGraph-Chatbot.git
cd GroundedGraph-Chatbot
npm install
```

### Environment variables

Create a `.env` file in the project root (see `.env.example`):

```
GEMINI_API_KEY=YOUR_GEMINI_API_KEY
PINECONE_API_KEY=YOUR_PINECONE_API_KEY
PINECONE_INDEX_NAME=agentic-ai-rag
PINECONE_HOST=YOUR_PINECONE_HOST
APP_URL=http://localhost:3000
```

Never commit the `.env` file.

### Run in development

```bash
npm run dev
```

### Build and run in production

```bash
npm run build
npm start
```

---

## API

### `POST /api/chat`

Request:

```json
{
  "message": "What is Agentic AI?"
}
```

The response contains the generated answer and the source page references used to produce it.

---

## Python Reference Implementation

The `python_submission/` folder contains a Python version of the same workflow using LangGraph, LangChain, Google Gemini, Pinecone, FastAPI and Uvicorn. The deployed application uses the TypeScript + Express implementation.

---

## Deployment

The app is deployed on Render: [langgraph-pinecone-rag-chatbot.onrender.com](https://langgraph-pinecone-rag-chatbot.onrender.com/)

---

## Security

- API keys are loaded from environment variables, never hard-coded.
- `.env` is listed in `.gitignore`; only `.env.example` is committed.
- If any credential was ever exposed (for example in an old commit), revoke and rotate it before using the project elsewhere.

---

## Roadmap

- Conversation memory for multi-turn follow-ups
- Streaming responses
- Persistent chat history
- Authentication
- Additional knowledge sources and expanded ingestion
- Retrieval and RAG evaluation metrics

---

## Author

**Supraja Putrevu**

B.Tech – Computer Science & Engineering (Data Science)

Python Developer | AI Enthusiast | Data Science | Machine Learning

GitHub: [https://github.com/UmaSupraja](https://github.com/UmaSupraja)
