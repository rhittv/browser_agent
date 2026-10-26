AI Browser Agent 🌐

An AI-powered browser automation project exploring how intelligent agents can interact with web environments, execute browser tasks, and automate repetitive workflows.

✨ Overview

The AI Browser Agent focuses on combining AI-driven decision-making with browser automation. The goal is to create a system that can interpret a task, interact with web pages, and perform actions through a structured automation workflow.

This project demonstrates practical exploration of AI agents beyond simple question-and-answer interactions.

🚀 Features

Browser Automation — Automate supported browser interactions.

Task-Oriented Workflows — Organize browser actions around a user-defined goal.

AI Integration — Connect language-model capabilities with automation logic.

Web Interaction — Work with page elements and browser interfaces through the configured automation tools.

Extensible Architecture — A foundation for adding more tools and automation capabilities.

🛠️ Tech Stack

Python

AI model/API integration

Browser automation tooling, depending on the project configuration

⚙️ How It Works

A typical agent workflow can be described in four stages:

Receive a task — The user specifies what they want the agent to accomplish.

Interpret the goal — The system processes the task and determines the next action.

Interact with the browser — The automation layer performs the supported browser operations.

Return the result — The system reports the outcome or continues the workflow as needed.

The exact behavior depends on the tools and execution logic implemented in the project.

📂 Project Structure

The codebase contains the components responsible for agent logic, AI integration, browser interaction, and task execution. Refer to the repository files for the actual modules and entry point.



# 🤖 Browser Agent — Setup Guide

## Quick Start (Windows)

### 1. Install dependencies (once)

Open **cmd.exe** (not PowerShell) and run:

```cmd
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
npm install -g @modelcontextprotocol/server-puppeteer
```

> ⚠️ If npm fails in PowerShell with "execution policy" error, use **cmd.exe** instead.

### 2. Set your API key

Open `.env` and paste your key:

```
ANTHROPIC_API_KEY=sk-ant-YOUR_KEY_HERE
```

Get your key at: https://console.anthropic.com → API Keys

### 3. Start

Double-click **`start.bat`** — or via cmd:

```cmd
venv\Scripts\activate
uvicorn server:app --reload --port 8000
```

### 4. Open in browser

http://localhost:8000

---

## Accounts

| Login | Password | Role          | Access               |
| ----- | -------- | ------------- | -------------------- |
| admin | admin123 | Administrator | All tasks, all users |
| alice | alice123 | User          | Own tasks only       |
| bob   | bob123   | User          | Own tasks only       |

---

## Project Structure

```
browser-agent/
├── server.py           # FastAPI server (entry point)
├── agent_core.py       # ReAct agent + Claude
├── database.py         # SQLite DB (users, tasks)
├── requirements.txt    # Python dependencies
├── .env                # API key
├── start.bat           # One-click start (Windows)
├── data/
│   └── agent.db        # Database (auto-created)
├── static/
│   └── index.html      # Web dashboard
├── tools/
│   ├── browser_tools.py # Browser control
│   └── dom_subagent.py  # AI element finder
├── utils/
│   ├── mcp_client.py    # MCP/Puppeteer client
│   └── logger.py        # Logger + WebSocket
└── config/
    └── system_prompts.py # Agent prompts
```

---

## Troubleshooting

### `npm` fails with "execution policy" error

Use **cmd.exe** instead of PowerShell, or run in PowerShell as admin:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### `MCP connection failed`

```cmd
node --version          # must be 18+
npm install -g @modelcontextprotocol/server-puppeteer
npx puppeteer browsers install chrome
```

### Port 8000 already in use

```cmd
uvicorn server:app --port 8001
```

Then open http://localhost:8001

### `ANTHROPIC_API_KEY not found`

Make sure the `.env` file exists in the project root and contains the correct key.

---

## How It Works

1. You enter a task in the web dashboard
2. FastAPI creates a record in SQLite and starts the agent in background
3. Agent (Claude Sonnet) runs the ReAct loop:
   - **THINK** → analyzes the task and page state
   - **ACT** → calls a browser tool (via MCP/Puppeteer)
   - **OBS** → observes the result
   - Repeats until task is complete (max 20 steps)
4. Each step is streamed via WebSocket in real time
5. Result is saved to DB and visible in task history

# browser_agent
