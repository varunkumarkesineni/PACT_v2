
---

## Core Features

### Phase 1 — Foundation & Security

| Feature | Description |
|---|---|
| **Authentication** | `bcrypt` password hashing, 12-character minimum policy, database-backed account lockout after 5 failed attempts |
| **Role-Based Access Control (RBAC)** | Authorization enforced at the backend service layer — not the UI — across 5 distinct roles |
| **Immutable Audit Logging** | Every login, access attempt, and privileged action is permanently recorded in MongoDB |

### Phase 2 — Investigation Management & Analytics

| Feature | Description |
|---|---|
| **FIR & Case Dossiers** | Full CRUD for First Information Reports; tracks Complainants, Victims, Suspects, Witnesses, and Property |
| **Physical Evidence System** | Server-side file storage with SHA-256 integrity validation and path-traversal protection |
| **Chain of Custody** | Auditable transfer log for physical/digital evidence between officers (timestamps, condition, reason) |
| **Semantic Similarity Search** | Uses `all-MiniLM-L6-v2` sentence embeddings to surface "Potentially Similar Cases" by MO/text — presented as an investigative lead, never as proof |
| **SP Crime Analytics Dashboard** | Superintendent-exclusive view with Pandas/Plotly charts and geographic crime mapping |
| **Automated Reporting** | On-demand PDF case dossiers and CSV exports via ReportLab |
| **Officer-to-Officer Data Isolation** | *(P0 security constraint)* An officer cannot view, edit, search, or report on another officer's cases without explicit authorization |

### Phase 3 — AI Investigative Assistance

| Feature | Description |
|---|---|
| **Gemini Integration** | Real-time case summaries, investigation briefs, timeline sequencing, and Q&A via the Google GenAI SDK |
| **Pre-Payload Authorization** | The AI only ever receives data the requesting officer is already permitted to view; secrets are stripped before transmission |
| **Hallucination Guardrails** | Prompt-level constraints prevent the model from inventing evidence, suspects, or declaring guilt; missing data is explicitly flagged |
| **AI Audit Trail** | Every generation is logged in `ai_analysis_history` with prompt version, model, and duration |

---

## Technology Stack

| Layer | Technology |
|---|---|
| **Frontend** | Python, Streamlit (custom dark/navy theme, multipage navigation) |
| **Backend** | Python services, Pandas, scikit-learn (TF-IDF fallback) |
| **Database** | MongoDB via PyMongo, idempotent seeding, secured indexes |
| **AI / ML** | Sentence Transformers (`all-MiniLM-L6-v2`), Google GenAI SDK (Gemini API) |
| **Analytics** | Pandas, Plotly |
| **Documents** | ReportLab (PDF/CSV generation) |
| **Security** | bcrypt, python-dotenv |

---

## Role Hierarchy

| Role | Typical Permissions |
|---|---|
| **ADMIN** | Full system access, user management |
| **Superintendent of Police (SP)** | Crime analytics dashboard, cross-case visibility |
| **Sub-Inspector (SI)** | FIR creation, case management within jurisdiction |
| **Investigating Officer (IO)** | Case investigation, evidence handling, AI assistance |
| **Constable** | FIR creation, field data entry |

---

## Security Model

- **Isolation-first design** — data isolation is enforced at the database query level, not filtered after retrieval
- **Least-privilege AI access** — the LLM layer never sees more than the requesting officer is cleared to see
- **Defense against file-based attacks** — SHA-256 validation and path-traversal protection on all evidence uploads
- **Full accountability** — every sensitive action (login, access, evidence transfer, report generation, AI query) is immutably logged

---

## Deployment

- **Application hosting:** Streamlit Cloud
- **Database hosting:** MongoDB Atlas

This combination provides global accessibility for demonstration purposes while keeping the deployment footprint minimal.

---

## Project Status

PACT is an active, phased build. Phases 1–3 (Security Foundation, Investigation Management, and AI Assistance) are implemented as described above.

---

*Built as a demonstration of secure, role-aware, AI-augmented system design for the law-enforcement domain.*
