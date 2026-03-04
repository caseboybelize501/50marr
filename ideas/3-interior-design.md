# Virtual Interior-Design Assistant

## Core Value Proposition
Upload a room photo → AI proposes furniture layout, color schemes, and 3D renderings.

## Front-end (UI)
Vue.js + WebGL/Three.js viewer (AR/3D)

## Back-end (Core)
Ruby on Rails (designer marketplace, orders) + MongoDB (design assets)

## AI Layer (LLaMA.cpp)
LLaMA.cpp (style-transfer, text-to-image generation for mock-ups)

## Typical Integrations & Ops
3D asset library (Sketchfab), Stripe for payments, Cloudflare Workers for edge caching, Docker for isolation.

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
The interior design assistant follows the standard full-stack skeleton with:

1. Front-end Vue.js app with WebGL/Three.js viewer for AR/3D visualization
2. API Gateway (Nginx/Traefik) routing requests to backend services
3. Ruby on Rails backend handling designer marketplace, orders, and user accounts
4. LLaMA Service wrapping llama.cpp for style transfer and text-to-image generation
5. MongoDB storing design assets, templates, and user preferences
6. Integration with 3D asset library (Sketchfab)
7. Stripe integration for payments
8. Cloudflare Workers for edge caching of static assets

### Design Workflow
1. User uploads room photo
2. LLaMA.cpp analyzes space and suggests furniture layouts
3. Backend generates color schemes and design suggestions
4. 3D mock-ups rendered using external tools
5. Results displayed in Vue.js UI with Three.js viewer
6. User can save designs or purchase recommended items