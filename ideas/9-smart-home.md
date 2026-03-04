# Smart-Home Voice Automation Hub

## Core Value Proposition
Natural-language control of lights, thermostats, security, etc.

## Front-end (UI)
React (voice UI, device dashboard)

## Back-end (Core)
Node / Express (device command router) + MongoDB (device registry)

## AI Layer (LLaMA.cpp)
LLaMA.cpp (NLU → intent extraction, command synthesis)

## Typical Integrations & Ops
MQTT broker (Mosquitto), Home Assistant integration, TLS everywhere, Docker-Swarm for high-availability.

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
The smart home hub follows the standard full-stack skeleton with:

1. Front-end React app with voice UI and device dashboard
2. API Gateway (Nginx/Traefik) routing requests to backend services
3. Node/Express backend handling device command routing and user accounts
4. LLaMA Service wrapping llama.cpp for NLU intent extraction and command synthesis
5. MongoDB storing device registry and user preferences
6. Integration with MQTT broker (Mosquitto) for device communication
7. Home Assistant integration for smart home control
8. TLS encryption for all communications
9. Docker-Swarm for high-availability deployment

### Smart Home Workflow
1. User speaks voice command to React UI
2. LLaMA.cpp extracts intent and synthesizes appropriate commands
3. Backend routes commands to correct MQTT devices
4. Results displayed in device dashboard
5. All interactions logged for analytics and troubleshooting