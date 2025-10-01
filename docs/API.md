# API Documentation

## Overview
Complete API documentation for Sara AI Commerce Support Advisor.

## Endpoints

### Chat API
- `POST /api/v1/chat/message` - Send message to AI advisor
- `GET /api/v1/chat/history` - Get conversation history
- `DELETE /api/v1/chat/session` - Clear current session

### Products API
- `GET /api/v1/products/search` - Search products
- `GET /api/v1/products/:id` - Get product details
- `GET /api/v1/products/categories` - Get product categories

### Health API
- `GET /health` - Basic health check
- `GET /health/detailed` - Detailed system status

## Authentication
- Session-based authentication
- Rate limiting per IP
- Request validation with Zod schemas

## Error Handling
- Standardized error responses
- Persian error messages
- HTTP status codes
- Error correlation IDs
