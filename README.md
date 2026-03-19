# Ecom Chat Engine

An intelligent e-commerce customer support chatbot backend powered by OpenAI's GPT-3.5 Turbo. Designed to integrate with online stores as a conversational AI assistant for handling customer inquiries.

## Features

- **OpenAI GPT-3.5 Turbo Integration** — Context-aware conversational responses for customer support
- **Session Management** — Per-session conversation history with automatic context windowing (last 10 messages)
- **Multi-Store Architecture** — Database schema supports multiple stores with individual configurations
- **Platform Connectors** — Schema-ready for WooCommerce and Shopify integration
- **API Key Authentication** — Secure endpoint access with per-request API key validation
- **Rate Limiting** — Configurable request throttling (100 requests per 15-minute window by default)
- **Docker Support** — Full Docker Compose setup with PostgreSQL for local development
- **CORS Configuration** — Configurable cross-origin resource sharing for frontend integration

## Tech Stack

| Component | Technology |
|-----------|------------|
| Runtime | Node.js, Express |
| AI Engine | OpenAI GPT-3.5 Turbo |
| Database | PostgreSQL (Supabase-compatible) |
| Containerization | Docker, Docker Compose |

## Prerequisites

- Node.js 16+
- Docker & Docker Compose (for local database)
- OpenAI API key

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/mhmalvi/ecom-chat-engine.git
cd ecom-chat-engine
```

### 2. Configure Environment

```bash
cp .env.example .env
```

Edit `.env` with your configuration:

```env
PORT=3000
API_KEY=your_secure_api_key
OPENAI_API_KEY=your_openai_api_key
ALLOWED_ORIGINS=http://localhost:3000
```

### 3. Start with Docker

```bash
docker-compose up -d
```

### 4. Run Database Migrations

```bash
node database/run-migrations.js
```

### 5. Start the Server

```bash
npm start
```

## API Reference

### Chat Endpoint

```
POST /api/chat
```

**Headers:**
| Header | Description |
|--------|-------------|
| `X-API-Key` | Your store API key |
| `Content-Type` | `application/json` |

**Request Body:**
```json
{
  "message": "What is your return policy?",
  "sessionId": "unique-session-id"
}
```

**Response:**
```json
{
  "reply": "Our return policy allows returns within 30 days...",
  "sessionId": "unique-session-id"
}
```

## Database Schema

The PostgreSQL schema includes the following tables:

- **stores** — Store configurations, API keys, bot settings, and platform credentials
- **users** — User accounts linked to stores with role-based access
- **messages** — Full conversation history with session tracking and JSONB metadata
- **orders** — Order records created through bot interactions

## Project Structure

```
ecom-chat-engine/
├── app.js                              # Express server and route definitions
├── database/
│   ├── migrations/
│   │   └── 001_initial_schema.sql      # Database schema
│   └── run-migrations.js               # Migration runner
├── docker-compose.yml                  # Docker services configuration
├── Dockerfile
├── .env.example                        # Environment variable template
└── package.json
```

## License

This project is open source and available under the [MIT License](LICENSE).
