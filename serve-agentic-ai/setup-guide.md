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

#### 1) Create virtual environment (one-time)

**Git Bash**

```bash
cd <REPO_DIR>
python -m venv .venv
source .venv/Scripts/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
deactivate

Repeat for all the three services (MCP server, Orchestrator, Agents)
```

#### 2) Create `.env` (one-time)

```bash
cp .env.example .env     # Git Bash
```

Then edit `.env` with the values for your local stack.

### 3) MCP Server&#x20;

```bash
cd C:\Serve-Agentic\serve-agentic-mcp-service
source .venv/Scripts/activate
uvicorn app:app --app-dir src --port 9000
```

### 4) Orchestrator

```bash
cd C:\Serve-Agentic\serve-vm-orchestrator
source .venv/Scripts/activate
export PYTHONPATH=src
python -m app.main
```

### 5) Agents Service

```bash
cd C:\Serve-Agentic\serve-vm-agents
source .venv/Scripts/activate
uvicorn service.main:app --app-dir src --port 8001
```

### 6) Streamlit Simulator (Local “Volunteer Chat UI”)

```bash
cd C:\Serve-Vriddhi\serve-agentic-dev-infra
source .venv/Scripts/activate
streamlit run app.py
```
