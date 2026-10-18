# PharmaAI — Intelligent Pharmaceutical Sales & Engagement Platform

<p align="center">
  <strong>Connecting Doctors, Pharmaceutical Companies, and Sales Representatives Through AI</strong>
</p>

...
## Overview

**PharmaAI** is an AI-powered pharmaceutical engagement platform designed to improve how doctors discover pharmaceutical products, how companies manage their sales operations, and how doctors connect with sales representatives.

The platform brings together conversational AI, Retrieval-Augmented Generation (RAG), product discovery, doctor–product matching, document intelligence, order management, and human sales conversations in one role-based application.

Rather than relying exclusively on a chatbot, PharmaAI combines AI-assisted interactions with structured backend tools, knowledge retrieval, safety checks, and human escalation workflows.

The goal is to make pharmaceutical engagement more organized, accessible, and efficient through intelligent automation and human collaboration.

## Live Deployment

| Component | Technology | Link |
|---|---|---|
| Frontend | Vercel | [Open PharmaAI](https://pharma-ai-sales-system-frontend.vercel.app/) |
| Backend API | FastAPI on Render | [API Documentation](https://pharma-ai-sales-system.onrender.com/docs) |
| Database | Neon PostgreSQL | Managed PostgreSQL |
| Source Code | GitHub | [View Repository](https://github.com/zubairkamran69/Pharma-Ai-system) |

> **Note:** Hosted services may take time to respond after periods of inactivity, depending on the hosting configuration.

## The Problem

Pharmaceutical engagement often involves disconnected workflows for product information, doctor relationships, sales communication, document access, and support requests.

PharmaAI brings these workflows together:

- Doctors can discover relevant product information and request human assistance.
- Pharmaceutical companies can manage products, knowledge documents, doctors, and sales representatives.
- Sales representatives can access relevant company information and communicate with doctors.
- Safety-sensitive questions can be directed to human review.
- Platform administrators can manage account verification and platform oversight.

## Key Features

### AI-Powered Conversational Supervisor

- Routes user requests to relevant application capabilities.
- Supports general conversation and product-related questions.
- Connects document retrieval, structured backend tools, safety handling, and human escalation.
- Supports configurable AI providers.
- Uses backend records and tools for structured commercial information such as products, prices, inventory, and orders rather than relying solely on model-generated answers.

### Retrieval-Augmented Generation (RAG)

- Supports authorized PDF, DOCX, TXT, and Markdown knowledge documents.
- Extracts and processes document text.
- Splits content into searchable chunks.
- Retrieves relevant passages using TF-IDF-based search.
- Provides retrieved context to the configured AI provider.
- Supports company-specific knowledge access and product knowledge retrieval.

### Doctor Workspace

- Doctor registration with professional information.
- Profile and verification-status management.
- Specialty-to-product matching.
- Product discovery and product requests.
- AI-assisted product information.
- Human sales representative contact.
- Conversation history and support workflows.

### Pharmaceutical Company Workspace

- Company registration and approval workflow.
- Company-scoped medicine and product management.
- Company-wide and medicine-specific document uploads.
- Doctor directory and specialty/product matching.
- Sales representative management.
- Orders, escalations, conversation history, and analytics.

### Sales Representative Workspace

- Company-managed account creation.
- Unique Sales ID and company association.
- Access to relevant company products and knowledge.
- Doctor conversations and related context.
- Human sales handoff and communication workflows.

Sales representatives are created through pharmaceutical company workflows rather than public self-registration.

### Private Owner Administration

- Review and manage doctor and company verification.
- View registered users and sales representatives.
- Review registration information and account statuses.
- Inspect platform document and escalation information.
- Respect access boundaries for private doctor-to-company sales conversations.

### Safety and Human Escalation

The application includes safety checks for designated high-risk scenarios, including emergencies, overdose, adverse events, pregnancy-related decisions, and patient-specific treatment questions.

These workflows can create human-review tickets and preserve relevant conversation context to support follow-up.

PharmaAI is a demonstration of safety-oriented application design and does not replace qualified clinical judgment.

## How It Works

```text
                    User Workspaces
                          |
          +---------------+----------------+
          |               |                |
        Doctor        Pharma Company    Sales Rep
          |               |                |
          +---------------+----------------+
                          |
                  Supervisor Agent
                          |
          +---------------+----------------+
          |               |                |
     RAG Retrieval   Structured Tools   Safety Checks
          |               |                |
     Approved Docs   Products / Orders   Human Review
          |               |                |
          +---------------+----------------+
                          |
                 Contextual Response
                          |
                  Human Sales Handoff
                          |
                  Doctor <-> Sales Rep
```

### Request Lifecycle

1. A user submits a question or performs an action in their workspace.
2. The backend identifies the relevant application workflow.
3. The supervisor routes the request to retrieval, structured tools, safety handling, or escalation as appropriate.
4. Retrieved documents or backend records provide relevant context.
5. When configured, the selected LLM generates a response using the available context.
6. Safety-sensitive requests can be directed to human review.
7. Product requests, orders, and conversations are handled through backend application workflows.

## Technology Stack

| Layer | Technology |
|---|---|
| Frontend hosting | Vercel |
| Backend framework | Python, FastAPI |
| Backend hosting | Render |
| Database | Neon PostgreSQL |
| Database connectivity | PostgreSQL through `DATABASE_URL` |
| Authentication | JWT-based authentication |
| Document processing | PDF, DOCX, TXT, Markdown |
| Retrieval | TF-IDF-based document retrieval |
| AI orchestration | Supervisor-style routing, RAG, tools, and safety workflows |
| LLM providers | Demo, Ollama, and OpenAI-compatible API |
| API interface | FastAPI OpenAPI / Swagger UI |
| Version control | Git and GitHub |

## AI Provider Configuration

PharmaAI supports three AI provider modes.

### 1. Demo Mode

```env
LLM_PROVIDER=demo
```

Uses an explicitly labeled extractive responder. This mode provides a demonstration of the application workflow and is not actual LLM inference.

### 2. Local LLM with Ollama

```env
LLM_PROVIDER=ollama
OLLAMA_BASE_URL=http://localhost:11434/api/chat
OLLAMA_MODEL=llama3.2:3b
```

Requires Ollama and a compatible model to be installed and accessible from the backend environment.

The localhost address is intended for local development. A hosted backend cannot directly access Ollama running on your personal computer through its own `localhost`.

### 3. OpenAI-Compatible API

```env
LLM_PROVIDER=openai
LLM_API_KEY=your_api_key
LLM_MODEL=gpt-4o-mini
LLM_BASE_URL=https://api.openai.com/v1/chat/completions
```

Requires a valid provider API key and compatible model. API usage may incur charges.

### AI Provider Error Handling

PharmaAI distinguishes between its explicitly configured demo mode and hosted or local LLM inference.

- Demo mode uses the extractive responder by design.
- Ollama and OpenAI-compatible modes use their configured provider.
- Provider errors should be surfaced through the relevant application error-handling path rather than silently presented as successful AI-generated answers.
- The application should not imply that a real LLM generated a response when the demo responder was used.

## Authentication and Verification

Public account registration is intended for doctors and pharmaceutical companies.

- Newly registered accounts can enter a pending verification state.
- The platform owner reviews accounts through the administration workflow.
- Sales representatives are created by verified companies.
- JWT authentication protects supported API operations.
- Company-specific document access is scoped to the relevant company.

For the Pakistan demonstration, doctor registration includes PM&DC-style professional registration information. This does not imply direct or authorized access to the PM&DC verification system.

The application supports an owner-approval workflow. Automated verification using credentials beginning with `DEMO-` can be enabled for testing through `DEMO_VERIFICATION=true`, where supported by the configured implementation.

## Database and Data Storage

PharmaAI uses **Neon PostgreSQL** as its application database. SQLite is not a runtime fallback.

The database stores application records and document metadata, including extracted text chunks. Uploaded document files currently reside on the backend filesystem.

The application uses its configured PostgreSQL connection through `DATABASE_URL`. Database connectivity and schema initialization should be confirmed in the backend logs and health endpoint after deployment.

## Run Locally on Windows

### Prerequisites

- Python 3.12 recommended for the current project setup.
- Git.
- A Neon PostgreSQL database.
- An appropriate LLM provider if actual model inference is required.

### 1. Clone the Repository

```powershell
git clone https://github.com/zubairkamran69/Pharma-Ai-system.git
cd Pharma-Ai-system
```

### 2. Create and Activate a Virtual Environment

```powershell
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install Dependencies

```powershell
pip install -r backend\requirements.txt
```

### 4. Configure Environment Variables

Copy the example environment file:

```powershell
Copy-Item .env.example .env
```

Update `.env` with your own configuration:

```env
DATABASE_URL=your_neon_postgresql_connection_string
JWT_SECRET=replace_with_a_random_secret_of_at_least_32_characters
CORS_ORIGINS=http://localhost:5173
LLM_PROVIDER=demo
```

Use the environment variable names expected by the application and add any other required settings documented in `.env.example`.

**Security:** Never commit `.env`, real credentials, database connection strings, or API keys to GitHub. If a real credential has been exposed, rotate it with the relevant provider.

### 5. Start the Backend

From the repository root:

```powershell
uvicorn backend.main:app --reload
```

The API should be available at:

- API: `http://127.0.0.1:8000`
- Swagger UI: `http://127.0.0.1:8000/docs`
- Health endpoint: `http://127.0.0.1:8000/api/health`

The backend uses the configured PostgreSQL database and its application schema initialization process.

### 6. Configure the Frontend

Run the frontend using the actual frontend directory and package scripts in the repository.

If the frontend uses Vite, the API base URL may be configured with:

```env
VITE_API_URL=http://127.0.0.1:8000
```

Use this variable only if the frontend source code reads `VITE_API_URL`. Otherwise, configure the environment variable already used by the project.

## Production Deployment

### Frontend — Vercel

1. Import the GitHub repository or its frontend directory into Vercel.
2. Configure the correct frontend root directory and build settings.
3. Add the frontend's expected backend URL environment variable.
4. Set its production value to the deployed Render API URL.
5. Redeploy after changing environment variables.

### Backend — Render

1. Connect the GitHub repository to Render.
2. Configure the Python environment and dependencies.
3. Set the backend working directory to match the repository structure.
4. Configure the ASGI start command for that directory.

If the working directory is `backend`:

```bash
uvicorn main:app --host 0.0.0.0 --port $PORT
```

If the working directory is the repository root:

```bash
uvicorn backend.main:app --host 0.0.0.0 --port $PORT
```

5. Configure `DATABASE_URL` with the Neon PostgreSQL connection string.
6. Set a secure `JWT_SECRET` containing at least 32 characters.
7. Set `CORS_ORIGINS` to the exact deployed frontend origin.
8. Configure the selected LLM provider and its required secrets.
9. Review deployment logs and check `/api/health`.

### Database — Neon

1. Create a Neon PostgreSQL project.
2. Generate a database connection string.
3. Store the connection string in Render environment variables, not in frontend code.
4. Confirm database connectivity through backend logs and the health endpoint.
5. Back up important data before schema changes.

Environment variable changes generally require a new deployment or restart to take effect.

## API Overview

| API group | Purpose |
|---|---|
| `/api/auth/*` | Authentication and registration |
| `/api/dashboard` | Role-specific dashboards |
| `/api/profile` | Professional profile management |
| `/api/medicines` | Product catalog |
| `/api/doctors` | Doctor directory and matching |
| `/api/reps` | Sales representative management |
| `/api/chat` | Conversational supervisor and AI workflows |
| `/api/contact-rep/{medicine_id}` | Human sales handoff |
| `/api/human-conversations/*` | Human conversation workflows |
| `/api/documents/{medicine_id}` | Medicine document uploads |
| `/api/company-documents` | Company knowledge uploads |
| `/api/rag/*` | Retrieval status and search |
| `/api/orders` | Product requests and orders |
| `/api/tickets` | Human escalation |
| `/api/admin/*` | Owner administration |

See the [interactive API documentation](https://pharma-ai-sales-system.onrender.com/docs) for the deployed API's available routes and schemas.

## Example AI Interactions

### Doctor

- "What medicines match my specialty?"
- "Tell me about Cardiovex 10."
- "What information came from the approved document?"
- "Connect me with a sales representative."

### Pharmaceutical Company

- "Show all new doctors."
- "Which doctors match Cardiovex 10?"
- "Show my sales representatives."
- "What is in my RAG knowledge base?"

Available responses depend on configured data, permissions, retrieved documents, and the selected AI provider.

## Safety, Privacy, and Responsible Use

PharmaAI is a hackathon and demonstration project, not a certified medical device or clinical decision-support system.

- Product information is not clinical guidance.
- Professional credentials require an authorized verification source for independent verification.
- Synthetic demo medicine information must not be used for treatment, prescribing, promotion, or regulatory decisions.
- Critical medical scenarios should be handled through qualified human review.
- Authentication, role-based authorization, and company-level isolation should be security-tested before production use.
- Secrets must remain in secure server-side environment variables.
- Uploaded documents must be authorized for their intended use.

The included `Cardiovex_10_Demo_Approved_Product_Profile.pdf` is fictional and intended to demonstrate document ingestion, retrieval, citations, routing, and escalation.

## Roadmap

Potential future enhancements include:

- Managed object storage for uploaded documents.
- pgvector embeddings and semantic retrieval.
- Versioned database migrations.
- Real-time messaging, notifications, and representative assignment enhancements.
- Repeatable synthetic seed data for larger demonstrations.
- Authorized professional credential verification integrations.
- Automated integration tests against a live Neon test database.
- Stronger audit logging, access-control testing, and production security review.

## Project Status

PharmaAI brings together AI-assisted pharmaceutical engagement, document retrieval, role-based workspaces, product workflows, and human sales communication in one platform.

Its architecture combines conversational AI with structured backend operations and human escalation, demonstrating how AI and application workflows can work together in a pharmaceutical engagement setting.

## Author

**Muhammad Zubair Kamran**

MERN Stack Developer | AI Enthusiast | Exploring Agentic AI and Intelligent Automation

- GitHub: [@zubairkamran69](https://github.com/zubairkamran69)
- LinkedIn: [Muhammad Zubair Kamran](https://linkedin.com/in/muhammad-zubair-kamran-32918735a)

---

<p align="center">
  <strong>PharmaAI — Bringing AI, pharmaceutical knowledge, and human engagement into one connected workflow.</strong>
</p>
