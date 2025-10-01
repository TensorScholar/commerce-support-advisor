# Architecture Documentation

## System Overview
Sara AI is a microservices-based architecture designed for Persian e-commerce support.

## Components

### Frontend (React Widget)
- **Technology**: React 18 + TypeScript + Vite
- **Features**: Shadow DOM, lazy loading, WebSocket
- **State Management**: Zustand
- **Styling**: Tailwind CSS with RTL support

### API Gateway (Node.js)
- **Technology**: Express.js + TypeScript
- **Features**: Rate limiting, validation, caching
- **Middleware**: CORS, Helmet, compression
- **Monitoring**: Winston logging, Sentry

### RAG Engine (Python)
- **Technology**: FastAPI + Python 3.12
- **Features**: Vector search, LLM integration
- **AI Models**: GPT-4 Turbo, Claude 3.5
- **NLP**: Hazm for Persian processing

### Data Layer
- **Vector DB**: Pinecone (embeddings)
- **Document DB**: MongoDB (conversations)
- **Cache**: Redis (3-tier caching)
- **Search**: Elasticsearch (keyword search)

## Data Flow
1. User sends message via widget
2. API Gateway validates and rate limits
3. RAG Engine processes with vector search
4. LLM generates response with context
5. Response validated against dataset
6. Sales strategy injected
7. Response cached and returned

## Security
- Input validation and sanitization
- Rate limiting and DDoS protection
- CORS and security headers
- Error handling without data leakage
