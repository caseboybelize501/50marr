# AI-Driven Stock-Trading Advisor

## Core Value Proposition
Predictive market analysis, strategy generation, and automated order placement.

## Front-end (UI)
Angular (real-time charts, alerts)

## Back-end (Core)
Python FastAPI service (trading engine) + PostgreSQL (positions, history)

## AI Layer (LLaMA.cpp)
LLaMA.cpp (trend summarization, strategy suggestion, risk-assessment text)

## Typical Integrations & Ops
Alpaca/Robinhood API for order execution, real-time market data feeds (Polygon.io), Redis for price cache, Prometheus alerts on model drift.

## Architecture Details

### LLaMA.cpp Configuration
- Model size: 7-B quantized GGML (q4_0 or q5_0)
- Quantization: q4_0 (or q5_0 if more precision needed)
- Batch size: 1-4 concurrent requests per instance
- Context window: 2048 tokens (default)
- Temperature: 0.7
- Max tokens: 256-512
- Streaming: Enabled for real-time UI

### Deployment Pattern
The stock trading advisor follows the standard full-stack skeleton with:

1. Front-end Angular app with real-time charts and alerts
2. API Gateway (Nginx/Traefik) routing requests to backend services
3. Python FastAPI backend handling trading engine and user accounts
4. LLaMA Service wrapping llama.cpp for trend summarization, strategy suggestion, and risk assessment
5. PostgreSQL storing positions, transaction history, and user data
6. Integration with Alpaca/Robinhood APIs for order execution
7. Real-time market data feeds from Polygon.io
8. Redis cache for price data
9. Prometheus monitoring for model drift alerts

### Trading Workflow
1. User accesses real-time charts and trading interface
2. LLaMA.cpp analyzes market trends and generates strategy suggestions
3. Backend executes trades through API integrations
4. Results displayed in Angular UI with charts and alerts
5. All transactions logged in PostgreSQL
6. Model drift monitoring via Prometheus alerts