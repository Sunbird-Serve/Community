# Setup Guide

#### **Prerequisites**

The following tools are required to run the SERVE Agentic System:

* **Docker Desktop** (required)\
  Used to run Kafka (Redpanda)
* **Python 3.10+** (required)\
  Used to run the orchestrator, agents, MCP server, and Streamlit simulator.
* **Git** (required)\
  Used to clone and manage the repositories.
* **Terminal / Shell**
  * Windows: Git Bash or PowerShell
  * macOS/Linux: Terminal

### 1) Infra: Redpanda (Kafka)

#### 1.1 Clone infra repo

```bash
cd C:\Serve-Agentic
git clone https://github.com/Sunbird-Serve/serve-agentic-dev-infra.git
cd serve-agentic-dev-infra
```

verify `docker-compose.yml`  in serve-agentic-dev-infra folder. Port to be used - 19092

#### 1.2 Start Infra

```bash
docker compose up -d
docker ps
```

You should see:

* `serve-redpanda`

#### Create required topics - One time

```bash
docker exec -it serve-redpanda rpk topic create serve.vm.whatsapp.in
docker exec -it serve-redpanda rpk topic create serve.vm.whatsapp.out
docker exec -it serve-redpanda rpk topic create serve.vm.onboarding
docker exec -it serve-redpanda rpk topic create serve.vm.dlq
```

Verify:

```bash
docker exec -it serve-redpanda rpk topic list
```

### Common one-time Python setup (per repo for MCP server, Orchestrator, Agents)

Repos - MCP server - git clone [https://github.com/Sunbird-Serve/serve-agentic-mcp-service.git](https://github.com/Sunbird-Serve/serve-agentic-mcp-service.git)

Orchestrator - git clone [https://github.com/Sunbird-Serve/serve-vm-orchestrator.git](https://github.com/Sunbird-Serve/serve-vm-orchestrator.git)

Agents - git clone [https://github.com/Sunbird-Serve/serve-vm-agents.git](https://github.com/Sunbird-Serve/serve-vm-agents.git)

Dev-Infra - git clone [https://github.com/Sunbird-Serve/serve-agentic-dev-infra.git](https://github.com/Sunbird-Serve/serve-agentic-dev-infra.git)

#### 1) Create virtual environment (one-time)

**Git Bash**

```bash
cd <REPO_DIR>
python -m venv .venv
source .venv/Scripts/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
deactivate

Repeat for all the four services (MCP server, Orchestrator, Agents, dev-infra)
```

### 2) MCP Server&#x20;

create .env file in C:\Serve-Agentic\serve-agentic-mcp-service and paste the below

```
# Broker
KAFKA_BROKERS=localhost:19092

# Topics
TOPIC_WA_OUT=serve.vm.whatsapp.out
TOPIC_WA_IN=serve.vm.whatsapp.in

# Service
MCP_PORT=9000
LLM_PROVIDER=claude
CLAUDE_API_KEY=api_key_here
CLAUDE_MODEL=model_here

WHATSAPP_PHONE_NUMBER_ID=phone_number_id_here
WHATSAPP_ACCESS_TOKEN=access_token_here
VERIFY_TOKEN=token_here
```

```bash
cd C:\Serve-Agentic\serve-agentic-mcp-service
source .venv/Scripts/activate
uvicorn app:app --app-dir src --port 9000
```

### 3) Orchestrator

create .env file in C:\Serve-Agentic\serve-vm-orchestrator and paste the below conf

```
KAFKA_BROKERS=localhost:19092
TOPIC_INBOUND=serve.vm.inbound
TOPIC_ONBOARDING=serve.vm.onboarding
SERVICE_NAME=vm-orchestrator
PORT=8000
```

```bash
cd C:\Serve-Agentic\serve-vm-orchestrator
source .venv/Scripts/activate
export PYTHONPATH=src
python -m app.main
```

### 4) Agents Service

create .env file in C:\Serve-Agentic\serve-vm-agents and paste the below

```
AGENT_NAME=onboarding
ONBOARDING_KAFKA_BROKERS=localhost:19092
ONBOARDING_TOPIC_ONBOARDING=serve.vm.onboarding
TOPIC_WA_IN=serve.vm.whatsapp.in
TOPIC_WA_OUT=serve.vm.whatsapp.out
ONBOARDING_GROUP_ID=vm-agent-onboarding
ONBOARDING_MCP_BASE=http://localhost:8080
ONBOARDING_PORT=8001
DATABASE_URL=postgresql+psycopg://user:password@localhost:5433/serve_agentic
```

```bash
cd C:\Serve-Agentic\serve-vm-agents
source .venv/Scripts/activate
uvicorn service.main:app --app-dir src --port 8001
```

### 5) Streamlit Simulator (Local “Volunteer Chat UI”)

create .env in C:\Serve-Vriddhi\serve-agentic-dev-infra and paste the below

```
KAFKA_BROKERS=localhost:19092
TOPIC_IN=serve.vm.whatsapp.in
TOPIC_OUT=serve.vm.whatsapp.out

WHATSAPP_PHONE_NUMBER_ID=phone_id_here
WHATSAPP_TOKEN=wa_token_here
VERIFY_TOKEN=verify_token_here

GRAPH_BASE=https://graph.facebook.com/v21.0
PORT=8088

```

```bash
cd C:\Serve-Vriddhi\serve-agentic-dev-infra
source .venv/Scripts/activate
streamlit run app.py
```
