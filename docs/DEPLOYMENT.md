# Deployment Guide

## Prerequisites
- Docker and Docker Compose
- Node.js 20+ and Python 3.12+
- API keys for OpenAI, Pinecone, MongoDB, Redis

## Environment Setup
1. Copy `env.example` to `.env`
2. Configure all required environment variables
3. Run `pnpm install` to install dependencies

## Development Deployment
```bash
# Start all services
pnpm run docker:up

# Build and start services
pnpm run docker:build
```

## Production Deployment
1. Configure production environment variables
2. Use `docker-compose.prod.yml`
3. Set up reverse proxy (Nginx)
4. Configure SSL certificates
5. Set up monitoring and logging

## Health Checks
- API Gateway: `http://localhost:3000/health`
- RAG Engine: `http://localhost:8000/health`
- MongoDB: Connection check
- Redis: Ping test

## Scaling
- Horizontal scaling with Docker Swarm
- Load balancing with Nginx
- Database clustering for high availability
