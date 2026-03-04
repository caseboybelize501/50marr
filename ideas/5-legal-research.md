# AI-Based Legal-Research SaaS

## Core Value Proposition
Search case law, get AI-written briefs, and receive argument suggestions.

## Front-end (UI)
React (search portal, document viewer)

## Back-end (Core)
Node / Express + Elasticsearch (full-text index) + PostgreSQL (user data)

## AI Layer (LLaMA.cpp)
LLaMA.cpp (case-law summarization, brief drafting, citation generation)

## Typical Integrations & Ops
Integration with Westlaw/LexisNexis APIs, OAuth2 SSO for law firms, Docker for sandboxed inference, GDPR-compliant logging.

## Architecture Details

### LLaMA.cpp Configuration
- Model size: 7-B quantized GGML (q4_0 or q5_0)
- Quantization: q4_0 (or q5_0 if more precision needed)
- Batch size: 1-4 concurrent requests per instance
- Context window: 2048 tokens (default)
- Temperature: 0.7 (0.5 for deterministic outputs like legal briefs)
- Max tokens: 256-512
- Streaming: Enabled for real-time UI

### Deployment Pattern
The legal research platform follows the standard full-stack skeleton with:

1. Front-end React app with search portal and document viewer
2. API Gateway (Nginx/Traefik) routing requests to backend services
3. Node/Express backend handling user authentication, search queries, and document management
4. LLaMA Service wrapping llama.cpp for case-law summarization and brief drafting
5. Elasticsearch for full-text indexing of legal documents
6. PostgreSQL storing user data, search history, and document metadata
7. Integration with Westlaw/LexisNexis APIs for document retrieval
8. OAuth2 SSO for law firm authentication
9. Docker containers for sandboxed inference environments

### Legal Research Workflow
1. User searches case law using natural language query
2. Backend queries Elasticsearch index and retrieves relevant documents
3. LLaMA.cpp summarizes cases and drafts legal briefs
4. Results displayed in React UI with document viewer
5. Users can download generated briefs or cite sources