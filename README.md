## PharmaAI — A Fully Integrated AI-Powered Platform

PharmaAI brings pharmaceutical engagement into one connected platform, combining intelligent conversational workflows, document-grounded knowledge retrieval, structured business operations, and direct human communication.

The system integrates doctor, pharmaceutical company, sales representative, and platform administrator workspaces through a centralized FastAPI backend and Neon PostgreSQL database, with the frontend deployed on Vercel.

### Integrated Capabilities

- **AI Conversational Assistant:** Context-aware interactions powered by a supervisor-style agent architecture.
- **Retrieval-Augmented Generation (RAG):** Document ingestion, relevant passage retrieval, and knowledge-grounded responses.
- **Doctor–Product Matching:** Specialty-oriented product discovery and recommendations based on available application data.
- **Pharmaceutical Company Management:** Company-scoped products, knowledge documents, doctor directories, and sales representative management.
- **Human Sales Conversations:** Direct doctor-to-representative communication and contextual handoff workflows.
- **Order Management:** Structured product requests and order-related operations.
- **Safety and Escalation:** Designated high-risk queries can be routed toward human review.
- **Role-Based Authentication:** Protected workflows for doctors, companies, sales representatives, and platform administrators.
- **Centralized Data Management:** PostgreSQL-backed application records through Neon.

## Intelligent Agent Architecture

PharmaAI is designed around a supervisor-style orchestration layer that directs requests to the appropriate capability instead of relying on a single keyword-based chatbot.

Depending on the request, the workflow can involve:

1. Intent and request routing.
2. Retrieval from relevant approved knowledge documents.
3. Structured application tools for products, doctors, representatives, and orders.
4. Safety checks and human-review workflows.
5. Contextual response generation through the configured AI provider.
6. Human sales handoff when direct representative interaction is needed.

This architecture connects conversational intelligence with practical application workflows, allowing the platform to support both information discovery and business operations.

## Deployment Architecture

| Component | Implementation |
|---|---|
| Frontend | Vercel |
| Backend | FastAPI on Render |
| Database | Neon PostgreSQL |
| Authentication | JWT-based authentication |
| Knowledge retrieval | TF-IDF-based RAG pipeline |
| AI integration | Configurable demo, Ollama, and OpenAI-compatible providers |
| API documentation | FastAPI OpenAPI / Swagger UI |

### Reliable AI Provider Handling

PharmaAI distinguishes between its explicitly configured response modes. In demo mode, the system uses an extractive responder rather than claiming to perform LLM inference. When a hosted AI provider is configured, provider errors are surfaced as errors instead of silently returning demo-generated responses.

This makes the selected AI mode clearer and helps developers identify configuration or provider issues.

## Project Experience

PharmaAI is designed as an integrated workflow rather than a standalone chatbot. Its user workspaces connect product discovery, document retrieval, account management, structured records, and human communication through a shared backend and database.

The deployed frontend and backend provide access to the platform's application workflows and API interface.

**Live Application:** [https://pharma-ai-sales-system-frontend.vercel.app/](https://pharma-ai-system-ccck.vercel.app/)

**Source Code:** [https://github.com/zubairkamran69/Pharma-Ai-system
](https://github.com/zubairkamran69/Pharma-Ai-system)
## Responsible Use

PharmaAI is an AI and pharmaceutical engagement demonstration platform. Product information and synthetic medicine documents are not clinical guidance. Safety-sensitive medical decisions require qualified professional review, and professional credentials should not be described as officially verified unless an authorized verification source is integrated.
