# AI-Enhanced Mental-Health Companion

## Core Value Proposition
24/7 empathetic chatbot, mood-tracking, and therapist hand-off.

## Front-end (UI)
Flutter (mobile, push notifications)

## Back-end (Core)
Flask API + PostgreSQL (sessions, user health data)

## AI Layer (LLaMA.cpp)
LLaMA.cpp (dialogue generation, sentiment analysis, coping-strategy suggestions)

## Typical Integrations & Ops
HIPAA-compliant hosting (AWS GovCloud), Twilio for SMS/voice, WebSocket for live chat, rate-limit middleware.

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
The mental health companion follows the standard full-stack skeleton with:

1. Front-end Flutter mobile app with push notifications
2. API Gateway (Nginx/Traefik) routing requests to backend services
3. Flask backend handling user sessions, health data, and chat interactions
4. LLaMA Service wrapping llama.cpp for dialogue generation and sentiment analysis
5. PostgreSQL storing user sessions, health data, and interaction history
6. Integration with Twilio for SMS/voice capabilities
7. WebSocket connections for live chat
8. Rate-limit middleware to prevent abuse
9. HIPAA-compliant hosting on AWS GovCloud

### Mental Health Workflow
1. User interacts with chatbot through Flutter app
2. LLaMA.cpp generates empathetic responses and analyzes sentiment
3. Backend tracks mood patterns and suggests coping strategies
4. If needed, system can suggest therapist hand-off
5. All interactions stored securely in PostgreSQL
6. Push notifications for reminders and check-ins