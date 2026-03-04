# Automated Video-Content Generator

## Core Value Proposition
Turn a short brief into a script, storyboard, and edited video clip.

## Front-end (UI)
Next.js (script editor, preview)

## Back-end (Core)
Django (project management) + S3 (raw/processed media)

## AI Layer (LLaMA.cpp)
LLaMA.cpp (scriptwriting, scene description, voice-over text)

## Typical Integrations & Ops
FFmpeg for video assembly, YouTube API for publishing, Celery workers for batch processing, autoscaling on K8s.

## Architecture Details

### LLaMA.cpp Configuration
- Model size: 7-B quantized GGML (q4_0 or q5_0)
- Quantization: q4_0 (or q5_0 if more precision needed)
- Batch size: 1-4 concurrent requests per instance
- Context window: 2048 tokens (default)
- Temperature: 0.7
- Max tokens: 256-512 (increase to 1024 for long-form content)
- Streaming: Enabled for real-time UI

### Deployment Pattern
The video generator follows the standard full-stack skeleton with:

1. Front-end Next.js app with script editor and preview functionality
2. API Gateway (Nginx/Traefik) routing requests to backend services
3. Django backend handling project management and user accounts
4. LLaMA Service wrapping llama.cpp for scriptwriting, scene description, and voice-over text generation
5. S3 storage for raw media files and processed video clips
6. Integration with FFmpeg for video assembly
7. YouTube API for publishing capabilities
8. Celery workers for batch processing of large video projects
9. Kubernetes autoscaling for handling traffic spikes

### Video Generation Workflow
1. User inputs content brief or topic
2. LLaMA.cpp generates script and scene descriptions
3. Backend orchestrates video creation using FFmpeg
4. Processed videos stored in S3
5. Results displayed in Next.js UI with preview functionality
6. Users can publish directly to YouTube