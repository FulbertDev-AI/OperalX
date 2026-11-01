# OperalX — AI Personal Assistant

<p align="center">
  <strong>An intelligent assistant powered by AI and Tool Calling</strong>
</p>

<p align="center">
  A modular AI assistant designed to interact with external services, automate tasks, retrieve information and help users manage their daily activities through natural language.
</p>

---

## Table of Contents

- [1. About the Project](#1-about-the-project)
- [2. Project Vision](#2-project-vision)
- [3. Main Objectives](#3-main-objectives)
- [4. Features](#4-features)
- [5. Available and Planned Integrations](#5-available-and-planned-integrations)
- [6. Technology Stack](#6-technology-stack)
- [7. System Architecture](#7-system-architecture)
- [8. Tool Calling Architecture](#8-tool-calling-architecture)
- [9. Project Structure](#9-project-structure)
- [10. Installation and Setup](#10-installation-and-setup)
- [11. Environment Configuration](#11-environment-configuration)
- [12. Running the Application Locally](#12-running-the-application-locally)
- [13. Available AI Tools](#13-available-ai-tools)
- [14. Streaming and Communication](#14-streaming-and-communication)
- [15. Security and Privacy](#15-security-and-privacy)
- [16. Testing](#16-testing)
- [17. Development Roadmap](#17-development-roadmap)
- [18. Deployment](#18-deployment)
- [19. Contributing](#19-contributing)
- [20. Author](#20-author)

---

## 1. About the Project

**OperalX** is an AI-powered personal assistant developed as part of the RodiumAI Bootcamp.

Unlike a traditional chatbot that only generates text responses, OperalX is designed to understand user requests, select appropriate tools, interact with external services and execute useful actions.

The assistant uses Large Language Models (LLMs) through the RodiumAI platform and an extensible Tool Calling architecture.

Users can interact with the assistant using natural language instead of manually navigating multiple applications.

The long-term goal is to create a unified AI assistant capable of managing everyday digital activities from a single conversational interface.

## 2. Project Vision

The vision behind OperalX is to make AI more useful in everyday life by connecting conversational intelligence with real-world applications.

Instead of simply answering questions, the assistant should be able to:

- Search for information on the Internet.
- Retrieve real-time information from external services.
- Manage personal calendar events.
- Assist with email communication.
- Access and organize documents.
- Interact with productivity platforms.
- Execute authorized actions on behalf of users.

OperalX aims to provide a modular, secure and extensible architecture where new capabilities can be integrated without redesigning the entire application.

## 3. Main Objectives

The project focuses on five main objectives:

**1. Natural Language Interaction**

Allow users to communicate with an AI assistant using simple, natural language.

**2. Intelligent Tool Selection**

Enable the AI model to determine when an external tool is necessary and select the appropriate tool based on the user's request.

**3. External Service Integration**

Connect the assistant to third-party services such as Google Calendar, Gmail, Notion and Google Drive.

**4. Secure Task Automation**

Ensure that sensitive operations require appropriate authorization and explicit user confirmation.

**5. Modular Architecture**

Build an extensible system that allows new tools, integrations and AI capabilities to be added independently.

---

## 4. Features

### 4.1 AI Conversational Assistant

- Natural language conversations.
- Integration with RodiumAI models.
- Context-aware responses.
- Conversation history.
- Streaming responses.
- Tool-assisted answers.

### 4.2 Tool Calling

OperalX uses a centralized tool registry to expose available capabilities to the AI model.

The model can:

1. Understand the user's request.
2. Determine whether a tool is required.
3. Select the appropriate tool.
4. Generate structured arguments.
5. Execute the tool through the backend.
6. Receive the tool result.
7. Generate a final response based on the result.

The system also validates tool arguments and handles execution errors.

### 4.3 Web Search

The assistant can retrieve information from the Internet using the Tavily Search API.

Capabilities include:

- General web searches.
- Information retrieval.
- Search result summaries.
- Source links.
- News searches.

Search results are returned to the AI model so it can generate answers based on retrieved information.

### 4.4 Weather Information

OperalX includes a weather tool within its Tool Calling architecture.

The current development implementation uses a local simulated weather response. It is intended to validate the tool execution workflow and can later be connected to a real weather provider.

### 4.5 Real-Time Streaming

The application uses Server-Sent Events (SSE) to stream assistant responses and communicate tool execution events.

This provides a more interactive conversational experience.

### 4.6 Conversation Management

The application supports conversation and message management through its backend persistence layer.

---

## 5. Available and Planned Integrations

OperalX is designed to integrate with multiple external services.

| Integration | Capabilities | Status |
|---|---|---|
| RodiumAI | LLM interaction and Tool Calling | Implemented |
| Tavily | Web search and news retrieval | Implemented |
| Weather | Weather tool execution | Local simulation |
| Google Calendar | Event management | In development |
| Gmail | Email search, drafts and sending | Planned |
| Notion | Search and page management | Planned |
| Google Drive | Document search and retrieval | Planned |

### 5.1 Google Calendar

The planned Google Calendar integration will allow users to manage their schedules through natural language.

Expected capabilities:

- Display upcoming events.
- Search events by date or period.
- Create calendar events.
- Update existing events.
- Delete events upon explicit user authorization.
- Handle dates, times and time zones.
- Ask clarification questions when information is missing.

Technology: Google Calendar API and OAuth 2.0.

### 5.2 Gmail

The planned Gmail integration will provide email assistance.

Expected capabilities:

- Search emails.
- Retrieve email information.
- Draft new messages.
- Send emails after explicit confirmation.

### 5.3 Notion

The planned Notion integration will support:

- Searching pages.
- Reading page content.
- Creating pages.
- Updating existing pages.

### 5.4 Google Drive

The planned Google Drive integration will support:

- Searching files.
- Retrieving document information.
- Reading supported documents.
- Providing document context to the AI assistant.

---

## 6. Technology Stack

### Backend

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| FastAPI | REST API framework |
| SQLAlchemy | Database ORM |
| Alembic | Database migrations |
| Pydantic | Data validation |
| RodiumAI | AI model access |
| Google APIs | External Google integrations |
| Tavily | Web search and news |

### Frontend

| Technology | Purpose |
|---|---|
| React 19 | User interface |
| TypeScript | Type safety |
| Vite | Development and build tooling |
| CSS | Interface styling |
| Server-Sent Events | Real-time streaming |

### Database

- PostgreSQL is the intended production database.
- SQLAlchemy provides database access and persistence.
- Alembic manages database schema migrations.

### Development Tools

- Git and GitHub.
- Visual Studio Code.
- Python virtual environments.
- npm.
- Pytest.
- Vitest.
- ESLint.

---

## 7. System Architecture

OperalX follows a frontend/backend architecture.

The frontend handles user interaction, while the backend manages AI communication, tool execution, external APIs, security and persistence.

### High-Level Architecture

```mermaid
flowchart TD
    A["User"] --> B["React Frontend"]
    B --> C["FastAPI Backend"]
    C --> D["Conversation Manager"]
    D --> E["RodiumAI LLM"]
    E --> F{"Tool Required?"}
    F -->|No| G["Generate Final Answer"]
    F -->|Yes| H["Tool Registry"]
    H --> I["Tool Execution"]
    I --> J["External Services"]
    J --> I
    I --> E
    E --> G
    G --> K["SSE Response"]
    K --> B
    C --> L["Database"]
```

### Backend Responsibilities

- Receive user messages.
- Manage conversations.
- Communicate with RodiumAI.
- Process model responses.
- Detect and execute tool calls.
- Validate tool arguments.
- Manage external API integrations.
- Stream responses through SSE.
- Persist conversations and messages.
- Enforce security policies.

### Frontend Responsibilities

- Display the conversational interface.
- Send messages to the backend.
- Display streamed responses.
- Display tool execution information.
- Display search sources.
- Manage conversation interactions.
- Handle loading and error states.

---

## 8. Tool Calling Architecture

Tool Calling is one of the central components of OperalX.

Instead of implementing each capability directly inside the conversation endpoint, the project uses a modular tool registry.

Each tool contains:

- A unique name.
- A description.
- A parameter schema.
- An execution function.
- An authorization policy.
- An execution timeout.

### Tool Execution Workflow

```mermaid
sequenceDiagram
    participant U as User
    participant F as Frontend
    participant B as FastAPI
    participant L as RodiumAI
    participant T as Tool Registry
    participant E as External API

    U->>F: Send a message
    F->>B: POST /chat
    B->>L: Message + available tools
    L-->>B: Tool call
    B->>T: Validate and execute tool
    T->>E: External API request
    E-->>T: Tool result
    T-->>B: Structured result
    B->>L: Tool result
    L-->>B: Final response
    B-->>F: SSE events
    F-->>U: Display answer
```

### Tool Registry

The registry is responsible for:

1. Registering available tools.
2. Exposing tool definitions to the model.
3. Validating tool arguments.
4. Enforcing authorization requirements.
5. Executing tools.
6. Handling execution errors and timeouts.

The architecture allows developers to introduce additional tools without rewriting the core conversation logic.

---

## 9. Project Structure

The project is organized into two main repositories.

### Backend Repository

`RODIUMAI-BOOTCAMP-bootcamp-chatbot-backend`

Main components include:

```text
backend/
├── main.py
├── llm_stream.py
├── tooling/
│   ├── __init__.py
│   ├── registry.py
│   ├── weather.py
│   └── search.py
├── tests/
├── prompts/
│   └── system.md
├── alembic/
├── .env.example
├── pyproject.toml
└── README.md
```

The actual repository may contain additional modules and files.

### Frontend Repository

`RODIUMAI-BOOTCAMP-bootcamp-chatbot-frontend`

Main components include:

```text
frontend/
├── src/
│   ├── api.ts
│   ├── sse.ts
│   ├── App.tsx
│   ├── App.css
│   └── components/
│       └── ChatWindow.tsx
├── public/
├── tests/
├── package.json
├── vite.config.ts
└── README.md
```

The actual repository may contain additional components and configuration files.

---

## 10. Installation and Setup

### Prerequisites

Before installing OperalX, make sure the following tools are installed:

- Python 3.14 or a compatible version supported by the project configuration.
- Node.js.
- npm.
- Git.
- PostgreSQL for a PostgreSQL-based setup.

You also need access to the RodiumAI platform to configure the model API credentials.

### 10.1 Clone the Backend

```bash
git clone https://github.com/FulbertDev-AI/RODIUMAI-BOOTCAMP-bootcamp-chatbot-backend.git

cd RODIUMAI-BOOTCAMP-bootcamp-chatbot-backend
```

### 10.2 Create a Python Virtual Environment

Windows:

```powershell
py -m venv .venv

.\.venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
python3 -m venv .venv

source .venv/bin/activate
```

### 10.3 Install Dependencies

```bash
python -m pip install -e .
```

If the repository provides another dependency installation method, follow its `pyproject.toml` or requirements instructions.

### 10.4 Configure Environment Variables

Copy the example configuration:

Windows:

```powershell
Copy-Item .env.example .env
```

Linux/macOS:

```bash
cp .env.example .env
```

Edit `.env` and configure the required credentials.

### 10.5 Database Configuration

Configure the database connection according to the environment variables expected by the backend.

Example PostgreSQL connection string:

```env
DATABASE_URL=postgresql+psycopg://username:password@localhost:5432/operalx
```

Install the appropriate PostgreSQL driver if it is not already included in the project dependencies.

Run migrations only after verifying the configured database and reviewing the available migration history:

```bash
alembic upgrade head
```

**Important:** Never run migrations against a database containing important data without first reviewing the migrations and creating a backup.

---

## 11. Environment Configuration

The backend uses environment variables to manage external service credentials and application configuration.

Example configuration:

```env
# Application
APP_ENV=development

# Database
DATABASE_URL=postgresql+psycopg://username:password@localhost:5432/operalx

# RodiumAI
RODIUMAI_API_KEY=your_rodiumai_api_key
RODIUMAI_BASE_URL=your_rodiumai_base_url

# AI Model
DEFAULT_MODEL=openai/gpt-4o

# Tavily Search
TAVILY_API_KEY=your_tavily_api_key

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_REDIRECT_URI=http://localhost:8000/auth/google