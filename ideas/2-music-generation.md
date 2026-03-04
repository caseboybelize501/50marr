# Personalized Music-Generation Service

## Core Value Proposition
AI-crafted playlists, custom lyrics, and short instrumental tracks.

## Front-end (UI)
Next.js (web) + React-Native (mobile)

## Back-end (Core)
Django REST Framework + MySQL (catalog, subscriptions)

## AI Layer (LLaMA.cpp)
LLaMA.cpp (lyrics generation, playlist curation, short audio-prompt description)

## Typical Integrations & Ops
Spotify/Apple Music API for licensing, Redis cache for popular playlists, S3 for generated audio files, CI/CD via GitHub Actions.

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
The music generation service follows the standard full-stack skeleton with:

1. Front-end Next.js web app and React-Native mobile app for user interaction
2. API Gateway (Nginx/Traefik) routing requests to backend services
3. Django REST Framework backend handling user accounts, playlist management, and subscription logic
4. LLaMA Service wrapping llama.cpp for lyrics generation and playlist curation
5. MySQL database storing user data, playlists, and subscription information
6. Redis cache for popular playlists and session management
7. S3 storage for generated audio files
8. Integration with Spotify/Apple Music APIs for licensing and metadata

### Music Generation Workflow
1. User inputs preferences (genre, mood, tempo)
2. LLaMA.cpp generates lyrics or musical descriptions
3. Backend orchestrates audio generation using external tools
4. Generated tracks stored in S3
5. Playlist updated in MySQL database
6. Cache invalidated and new playlist served to user