# Architecture

  ## Architecture Overview

  **Human Resources Escalation Triage** uses a React frontend, FastAPI backend, SQL persistence, retrieval-aware pipeline, and optional LLM provider. The architecture is intentionally small enough for students to run locally but structured enough to explain in interviews.

  - Selected architecture: Real Estate Policy Assistant
  - Template path: templates/simple-rag/real-estate-policy-assistant
  - Blueprint note: Use a microservices architecture to improve scalability and maintainability
  - Blueprint note: Implement a caching layer to improve performance
  - Blueprint note: Use a message queue to handle asynchronous tasks

  ## System Architecture Diagram

  ```mermaid
  flowchart LR
USER[User] --> UI[React Frontend]
UI --> API[FastAPI API]
API --> PIPE[Simple RAG Pipeline]
PIPE --> VECTOR[(Vector store)]
VECTOR --> PIPE
PIPE --> SERVICE[Service workflow]
SERVICE --> REVIEW[Validation and synthesis]
PIPE --> DB[(Run Log Database)]
REVIEW --> OUT[Human Resources Escalation Triage Answer]
OUT --> UI
  ```

  ## Component Responsibilities

  - Frontend layer: captures questions, shows answers, sources, and timeline.
  - Backend layer: validates requests, exposes API routes, handles errors.
  - AI/LLM layer: optional provider call with local deterministic fallback.
  - RAG/vector layer: retrieves relevant chunks when the project type needs retrieval.
  - Database layer: stores run logs and explainability evidence.
  - Background worker layer: recommended production upgrade for long tasks.
  - External services: optional OpenAI/Pinecone or deployment provider.

  ## Implementation Map

  - `backend/app/main.py`: FastAPI app, API routes, and request contract.
  - `backend/app/services/pipeline.py`: project workflow, retrieval, timeline, fallback handling, and answer synthesis.
  - `backend/app/domain.py`: domain profile, workflow steps, rules, starter questions, and tool catalog.
  - `backend/app/models.py`: SQL run-log model used for portfolio and debugging evidence.
  - `frontend/src/App.jsx`: learner-facing workspace and generated project UI.
  - `docs/PROJECT_DESIGN.md`: full problem statement, DFDs, database schema, APIs, and interview explanation.

  ## Component Diagram

  ```mermaid
  flowchart TB
UI[React App] --> CLIENT[API Client]
CLIENT --> ROUTE[FastAPI Routes]
ROUTE --> PIPELINE[Pipeline Service]
PIPELINE --> SEARCH[Vector/Search Service]
PIPELINE --> LLM[LLM/Fallback Service]
PIPELINE --> TOOLS[Tools and Domain Rules]
PIPELINE --> STORE[(SQL Run Logs)]
  ```

  ## Request Lifecycle

  ```mermaid
  sequenceDiagram
participant U as User
participant UI as React UI
participant API as FastAPI
participant P as Pipeline
participant S as Search
participant DB as Database
U->>UI: Submit question
UI->>API: POST /api/ask
API->>P: Validate and run workflow
P->>S: Retrieve context
S-->>P: Relevant chunks
P->>DB: Store run log
P-->>API: Answer, sources, timeline
API-->>UI: JSON response
UI-->>U: Render result
  ```

  ## Error Flow

  Provider or retrieval failures should return a friendly fallback response, preserve request context, and store a timeline step explaining the fallback mode without exposing secrets.

  ## Observability

  Track request latency, retrieval count, fallback mode, validation errors, and provider availability.

  ## Deployment Topology

  React can be served from Vercel/Nginx, FastAPI from Render/Railway/Docker, PostgreSQL as managed storage, and Chroma/Pinecone as a separate vector service for production datasets.
