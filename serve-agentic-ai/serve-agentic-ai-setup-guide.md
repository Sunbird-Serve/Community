# Serve Agentic AI - Setup Guide

### Prerequisites

* Docker & Docker Compose (v2.x+)
* Git
* A valid Anthropic API key (for LLM features)

### Quick Start

#### 1. Clone the repository

```bash
git clone <repo-url>
cd serve-ai
```

#### 2. Configure environment variables

Copy the example env file and fill in the required values:

```bash
cp .env.example .env
```

Edit `.env` and set:

```env
# Required — LLM API key (Anthropic Claude)
EMERGENT_LLM_KEY=sk-ant-api03-your-key-here

# Optional — WhatsApp Cloud API (for WhatsApp channel)
WHATSAPP_TOKEN=your-whatsapp-token
WHATSAPP_PHONE_NUMBER_ID=your-phone-number-id
WHATSAPP_APP_SECRET=your-app-secret

# Optional — Firebase (for volunteer auth during registration)
FIREBASE_API_KEY=your-firebase-web-api-key

# Optional — Teaching language for selection agent (default: English)
TEACHING_LANGUAGE=English
```

#### 3. Start all services

```bash
docker-compose up --build
```

This starts:

| Service                         | Port | Description                       |
| ------------------------------- | ---- | --------------------------------- |
| serve-ai-ui                     | 3000 | React frontend                    |
| serve-orchestrator              | 8001 | Central coordination layer        |
| serve-onboarding-agent-service  | 8002 | Volunteer onboarding              |
| serve-mcp-server                | 8004 | MCP server + PostgreSQL interface |
| serve-need-agent-service        | 8005 | Need coordination                 |
| serve-engagement-agent-service  | 8006 | Volunteer engagement              |
| serve-fulfillment-agent-service | 8007 | Volunteer-to-need matching        |
| serve-selection-agent-service   | 8009 | Post-onboarding evaluation        |
| postgres                        | 5433 | PostgreSQL database               |

#### 4. Access the application

* **Volunteer UI**: http://localhost:3000
* **Internal Staff Portal**: http://localhost:3000/internal
* **Orchestrator Health**: http://localhost:8001/api/health
* **MCP Server Health**: http://localhost:8004/api/health

#### 5. Verify all services are healthy

```bash
curl http://localhost:8001/api/health
curl http://localhost:8002/api/health
curl http://localhost:8004/api/health
curl http://localhost:8005/api/health
curl http://localhost:8006/api/health
curl http://localhost:8007/api/health
curl http://localhost:8009/api/health
```

All should return `{"status": "healthy"}`.

### Architecture Overview

```
Frontend (3000) → Orchestrator (8001) → Agents → MCP Server (8004) → PostgreSQL
                                                                    → Serve Registry (external)
```

The orchestrator routes requests to the appropriate agent based on persona detection:

* New volunteers → Onboarding → Selection → Engagement → Fulfillment
* Returning volunteers → Engagement → Fulfillment
* Recommended volunteers → Engagement (recommended handler) → Fulfillment
* Need coordinators → Need Agent

### Service-Specific Configuration

#### Onboarding Agent (Port 8002)

Videos for orientation are served from `serve-onboarding-agent-service/media/`:

* `welcome.mp4` — Coordinator welcome video
* `serve_class_intro.mp4` — Classroom demo video

#### MCP Server (Port 8004)

Connects to external Serve Registry at `https://serve-v1.evean.net`. Override with:

```env
SERVE_BASE_URL=https://serve-v1.evean.net
```

Database is auto-initialized on first start. Migrations run automatically.

#### Selection Agent (Port 8009)

Configure teaching language:

```env
TEACHING_LANGUAGE=Hindi
```

### Development

#### Rebuilding a single service

```bash
docker-compose up --build serve-onboarding-agent-service
```

#### Viewing logs for a specific service

```bash
docker-compose logs -f serve-orchestrator
docker-compose logs -f serve-onboarding-agent-service
docker-compose logs -f serve-mcp-server
```
