# 🎯 Sara AI - Commerce Support Advisor

## 📋 Project Overview

Sara AI is an intelligent commerce support advisor designed specifically for Persian language e-commerce platforms. The system provides real-time product recommendations, customer support, and sales assistance through an embeddable chat widget.

## 🏗️ Architecture

### Layer 1: Presentation (React Widget)
- **Shadow DOM** for CSS isolation
- **Lazy Loading** with route-based code splitting
- **WebSocket** for real-time streaming
- **Zustand** for state management

### Layer 2: API Gateway (Node.js)
- **Rate Limiting** with token bucket algorithm
- **Request Validation** using Zod schemas
- **Response Caching** with 3-tier strategy
- **Circuit Breaker** pattern for resilience

### Layer 3: Intelligence Core (Python RAG)
- **Persian Text Normalization** using Hazm
- **Hybrid Search** (Semantic + BM25)
- **LLM Integration** (GPT-4 + Claude fallback)
- **Response Validation** against dataset

### Layer 4: Data Storage
- **Pinecone** for vector embeddings
- **MongoDB** for conversation history
- **Redis** for caching
- **Elasticsearch** for keyword search

## 📁 Project Structure

```
sara-ai/
│
├─ apps/
│  └─ widget/                      # React TypeScript Widget
│     ├─ public/
│     │  ├─ embed.js               # Loader script (<10KB)
│     │  └─ widget-bundle.js       # Main bundle
│     ├─ src/
│     │  ├─ components/            # React components
│     │  │  ├─ ChatWindow.tsx      # Main chat container
│     │  │  ├─ MessageList.tsx     # Message history display
│     │  │  ├─ MessageInput.tsx    # Input field with send button
│     │  │  ├─ ProductCard.tsx     # Product display component
│     │  │  └─ TypingIndicator.tsx # Loading animation
│     │  ├─ hooks/                 # Custom React hooks
│     │  │  ├─ useChat.ts          # Chat state management
│     │  │  ├─ useWebSocket.ts     # Real-time connection
│     │  │  └─ useAnalytics.ts     # Event tracking
│     │  ├─ store/
│     │  │  └─ chatStore.ts        # Zustand store
│     │  ├─ services/
│     │  │  └─ apiClient.ts        # HTTP client wrapper
│     │  ├─ utils/
│     │  │  ├─ persian.ts          # Persian text utilities
│     │  │  └─ formatters.ts       # Data formatting helpers
│     │  ├─ types/
│     │  │  └─ index.ts            # TypeScript definitions
│     │  ├─ App.tsx                # Main app component
│     │  └─ main.tsx               # Entry point
│     ├─ package.json              # Dependencies and scripts
│     ├─ vite.config.ts            # Build configuration
│     └─ tsconfig.json             # TypeScript config
│
├─ services/
│  ├─ api-gateway/                 # Node.js Express Gateway
│  │  ├─ src/
│  │  │  ├─ middleware/            # Express middleware
│  │  │  │  ├─ rateLimit.ts        # Rate limiting logic
│  │  │  │  ├─ validation.ts       # Request validation
│  │  │  │  ├─ errorHandler.ts     # Global error handling
│  │  │  │  └─ logger.ts           # Winston logging
│  │  │  ├─ routes/                # API routes
│  │  │  │  ├─ chat.routes.ts      # Chat endpoints
│  │  │  │  ├─ products.routes.ts  # Product search
│  │  │  │  └─ health.routes.ts    # Health check
│  │  │  ├─ controllers/           # Business logic
│  │  │  │  ├─ chatController.ts   # Chat handling
│  │  │  │  └─ productsController.ts # Product operations
│  │  │  ├─ services/              # Service layer
│  │  │  │  ├─ ragService.ts       # RAG engine client
│  │  │  │  ├─ cacheService.ts     # Redis operations
│  │  │  │  └─ conversationService.ts # MongoDB operations
│  │  │  ├─ utils/
│  │  │  │  ├─ logger.ts           # Logging utilities
│  │  │  │  └─ validator.ts        # Validation helpers
│  │  │  ├─ config/
│  │  │  │  └─ index.ts            # Environment config
│  │  │  ├─ types/
│  │  │  │  └─ index.ts            # TypeScript definitions
│  │  │  ├─ app.ts                 # Express app setup
│  │  │  └─ server.ts              # Server startup
│  │  ├─ tests/                    # Test suites
│  │  │  ├─ unit/                  # Unit tests
│  │  │  └─ integration/           # Integration tests
│  │  ├─ package.json              # Dependencies
│  │  ├─ tsconfig.json             # TypeScript config
│  │  └─ Dockerfile                # Container config
│  │
│  ├─ rag-engine/                  # Python FastAPI RAG
│  │  ├─ src/
│  │  │  ├─ retrieval/             # Search components
│  │  │  │  ├─ vectorSearch.py     # Pinecone vector search
│  │  │  │  └─ fusionSearch.py     # Hybrid search (Phase 2)
│  │  │  ├─ preprocessing/         # Text processing
│  │  │  │  ├─ normalizer.py       # Persian normalization
│  │  │  │  └─ spellCorrector.py   # Spell correction
│  │  │  ├─ postprocessing/        # Response processing
│  │  │  │  ├─ validator.py        # Response validation
│  │  │  │  └─ salesStrategy.py    # Sales recommendations
│  │  │  ├─ llm/
│  │  │  │  └─ client.py           # LLM API clients
│  │  │  ├─ embeddings/
│  │  │  │  └─ embedder.py         # Embedding generation
│  │  │  ├─ utils/
│  │  │  │  └─ persian.py          # Persian utilities
│  │  │  ├─ config.py              # Configuration
│  │  │  └─ main.py                # FastAPI application
│  │  ├─ tests/                    # Test suites
│  │  ├─ requirements.txt          # Python dependencies
│  │  ├─ Dockerfile                # Container config
│  │  └─ pyproject.toml            # Python project config
│  │
│  └─ analytics/                   # Phase 3 - Analytics Service
│     └─ (deferred to Phase 3)
│
├─ data/
│  ├─ raw/                         # Source datasets
│  │  ├─ dataset.json              # Product dataset
│  │  └─ unified_knowledge.jsonld  # Knowledge base
│  ├─ processed/                   # Processed data
│  │  ├─ products_embedded.json    # Generated embeddings
│  │  ├─ faqs_embedded.json        # FAQ embeddings
│  │  └─ index_metadata.json       # Index metadata
│  ├─ validation/                  # Test data
│  │  ├─ test_queries.json         # Test queries
│  │  └─ expected_responses.json   # Expected responses
│  └─ scripts/                     # Data processing
│     ├─ 1_validate_dataset.py     # Dataset validation
│     ├─ 2_generate_embeddings.py  # Embedding generation
│     ├─ 3_upload_to_pinecone.py   # Vector upload
│     └─ 4_test_retrieval.py       # Retrieval testing
│
├─ infrastructure/
│  ├─ docker/                      # Container configs
│  │  ├─ docker-compose.yml        # Development setup
│  │  ├─ docker-compose.prod.yml   # Production setup
│  │  ├─ Dockerfile.gateway        # API Gateway image
│  │  └─ Dockerfile.rag            # RAG Engine image
│  └─ kubernetes/                  # Phase 4 - K8s configs
│     └─ (deferred to Phase 4)
│
├─ tests/                          # Test suites
│  ├─ e2e/                         # End-to-end tests
│  │  └─ chat_flow.spec.ts         # Playwright tests
│  └─ performance/                 # Load testing
│     └─ load_test.js              # K6 load tests
│
├─ docs/                           # Documentation
│  ├─ API.md                       # API documentation
│  ├─ DEPLOYMENT.md                # Deployment guide
│  ├─ ARCHITECTURE.md              # Architecture details
│  └─ RUNBOOK.md                   # Operations runbook
│
├─ .github/                        # GitHub workflows
│  └─ workflows/
│     ├─ ci.yml                    # Continuous integration
│     └─ cd.yml                    # Continuous deployment
│
├─ package.json                    # Monorepo configuration
├─ pnpm-workspace.yaml             # PNPM workspace config
├─ turbo.json                      # Turbo build config
├─ .gitignore                      # Git ignore rules
├─ env.example                     # Environment variables template
└─ LICENSE                         # MIT License
```

## 🚀 Implementation Phases

### Phase 1: MVP Foundation (Week 1-3)
**Goal**: Working chatbot with accurate responses

#### Week 1: Data Pipeline
- Validate and clean datasets
- Generate embeddings using OpenAI
- Upload vectors to Pinecone
- Test retrieval accuracy

#### Week 2: Backend Core
- Build RAG engine with FastAPI
- Create API gateway with Express
- Implement caching with Redis
- Set up MongoDB for conversations

#### Week 3: Frontend Widget
- Build React widget with Shadow DOM
- Implement chat interface
- Add Persian language support
- Create embeddable loader script

### Phase 2: Intelligence Enhancement (Week 4-5)
**Goal**: Production-ready accuracy & features

#### Week 4: Advanced RAG
- Implement hybrid search (semantic + BM25)
- Add spell correction for Persian
- Inject sales strategy recommendations
- Add conversation memory

#### Week 5: Testing & Polish
- Comprehensive test suite
- E2E testing with Playwright
- Performance optimization
- Error handling improvements

### Phase 3: Production Hardening (Week 6-7)
**Goal**: Deploy to production with monitoring

#### Week 6: Observability
- Structured logging with Winston
- Metrics collection with Prometheus
- Error tracking with Sentry
- Health check endpoints

#### Week 7: Deployment
- Docker containerization
- Production environment setup
- CI/CD pipeline
- Documentation completion

### Phase 4: Scale & Optimize (Week 8+)
**Goal**: Handle 10K+ users, reduce costs

- Horizontal scaling with Kubernetes
- CDN integration
- Database optimization
- Local LLM deployment
- Advanced analytics

## 🛠️ Technology Stack

### Frontend
- **React 18** + TypeScript 5
- **Vite** for building
- **Zustand** for state management
- **Tailwind CSS** for styling
- **Axios** for HTTP requests

### Backend
- **Node.js 20** + Express 4
- **Python 3.12** + FastAPI 0.110
- **Zod** for validation (Node)
- **Pydantic** for validation (Python)

### AI/ML
- **OpenAI GPT-4 Turbo** (primary LLM)
- **Anthropic Claude 3.5** (fallback)
- **text-embedding-3-large** (embeddings)
- **Pinecone** (vector database)
- **Hazm** (Persian NLP)

### Data
- **MongoDB 7** (conversations)
- **Redis 7** (caching)
- **Elasticsearch 8** (keyword search)

### DevOps
- **Docker** + Docker Compose
- **GitHub Actions** (CI/CD)
- **Prometheus** + **Grafana** (monitoring)
- **Sentry** (error tracking)

## 📊 Expected Metrics (MVP)

### Performance
- Response Time (p95): < 2.5s
- Response Time (p99): < 5s
- Throughput: 100 concurrent users
- Widget Load Time: < 2s

### Quality
- Accuracy: > 90%
- Hallucination Rate: < 1%
- User Satisfaction: > 80%
- Sales Conversion Lift: +15%

### Reliability
- Uptime: 99.5%
- Error Rate: < 1%
- MTTR: < 15min

### Cost (Monthly)
- OpenAI API: ~$200
- Pinecone: Free tier
- MongoDB: Free tier
- Infrastructure: $50
- **Total: ~$250/month**

## 🔧 Critical Implementation Guidelines

### 1. Dataset Fidelity (Non-Negotiable)
- Every LLM response must be validated against dataset
- Confidence threshold: 0.85
- Reject responses not traceable to source data

### 2. Persian Language Processing
- Normalize text before retrieval
- Handle character variations (ی/ي, ک/ك)
- Support RTL text display

### 3. Caching Strategy
- L1: In-Memory (5min TTL)
- L2: Redis (1hr TTL)
- L3: Database (persistent)

### 4. Error Handling
- Exponential backoff for retries
- Graceful fallbacks for all components
- Comprehensive logging

### 5. Sales Strategy
- Rule-based post-processing
- Not dependent on LLM generation
- Upsell/cross-sell recommendations

## 🚦 Getting Started

### Prerequisites
- Node.js 20+
- Python 3.12+
- Docker & Docker Compose
- PNPM 8+

### Environment Setup
1. Clone repository
2. Copy `env.example` to `.env`
3. Configure API keys
4. Run `pnpm install`
5. Start with `pnpm run docker:up`

### Development
```bash
# Install dependencies
pnpm install

# Start development servers
pnpm run dev

# Run tests
pnpm run test

# Build for production
pnpm run build
```

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Commit changes
4. Push to branch
5. Create Pull Request

## 📞 Support

For support and questions:
- Create an issue on GitHub
- Contact: [TensorScholar](https://github.com/TensorScholar)

---

**Sara AI** - Intelligent Commerce Support for Persian E-commerce Platforms
