# Nexora AI

### Agentic RAG Conversational Platform

Nexora AI is an agentic conversational AI platform built with **LangGraph, Gemini, LangChain, and Retrieval-Augmented Generation (RAG)**. It combines intelligent tool selection, document-based knowledge retrieval, persistent conversation memory, and human-in-the-loop workflows into a single conversational system.

---

## ✨ Features

- 🤖 **Agentic AI Chatbot** — Uses LangGraph to orchestrate multi-step conversations and tool execution.
- 🧠 **Gemini-Powered LLM** — Uses Google's Gemini models for intelligent response generation.
- 📚 **RAG Pipeline** — Upload PDFs, process documents, generate embeddings, and retrieve relevant information using vector search.
- 🔎 **Vector Search** — Uses FAISS for semantic document retrieval.
- 🛠️ **Tool Calling** — Supports external tools for web search, calculations, weather, stock information, and other actions.
- 💾 **Conversation Memory** — Persists conversation state and enables users to continue previous conversations.
- 🧑‍💻 **Human-in-the-Loop** — Sensitive actions can pause execution and require explicit human approval before continuing.
- ⚡ **Streaming Responses** — Streams AI responses and tool execution status in real time.
- 🐳 **Dockerized** — Includes Docker configuration for reproducible application deployment.
- 🔄 **CI/CD** — GitHub Actions workflow automates application build and deployment.
- 📊 **Multi-Conversation Support** — Maintains independent conversation threads for different sessions.

---

## 🏗️ Architecture

```text
                         ┌─────────────────────┐
                         │    Streamlit UI     │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   LangGraph Agent   │
                         └──────────┬──────────┘
                                    │
                       ┌────────────┴────────────┐
                       │                         │
                       ▼                         ▼
                ┌─────────────┐           ┌─────────────┐
                │ Gemini LLM  │           │ Tool Layer  │
                └─────────────┘           └──────┬──────┘
                                                 │
                         ┌───────────────────────┼──────────────────┐
                         │                       │                  │
                         ▼                       ▼                  ▼
                    RAG Search              Web Search         Other Tools
                         │
                         ▼
                  ┌─────────────┐
                  │ FAISS Index │
                  └──────┬──────┘
                         │
                         ▼
                 Uploaded Documents
🔄 Agent Workflow
User submits a query through the Streamlit interface.
LangGraph maintains the conversation state.
Gemini determines whether the request can be answered directly or requires a tool.
If a tool is required, LangGraph routes the request to the appropriate tool.
For document-related questions, the RAG pipeline retrieves relevant document chunks.
Tool results are returned to the agent.
The agent generates the final response.
Sensitive actions can trigger a human approval step before execution.
Conversation state is persisted using LangGraph checkpointing.
📚 RAG Pipeline

Nexora AI supports document-based question answering through a retrieval-augmented generation pipeline.

PDF Upload
    ↓
Document Loading
    ↓
Text Chunking
    ↓
Gemini Embeddings
    ↓
FAISS Vector Store
    ↓
Semantic Retrieval
    ↓
Relevant Context
    ↓
Gemini LLM
    ↓
Grounded Response

Documents are split into overlapping chunks before being converted into embeddings and stored in a FAISS vector index.

🛠️ Technology Stack
Category	Technologies
Language	Python
LLM	Google Gemini
Agent Framework	LangGraph
LLM Framework	LangChain
RAG	LangChain, PyPDF
Embeddings	Google Generative AI Embeddings
Vector Database	FAISS
UI	Streamlit
Memory	SQLite / LangGraph Checkpointing
Containerization	Docker
CI/CD	GitHub Actions
📁 Project Structure
Nexora-AI/
│
├── .github/
│   └── workflows/
│       └── cicd.yaml
│
├── app.py
├── backend.py
├── Dockerfile
├── requirements.txt
├── .dockerignore
├── .gitignore
├── LICENSE
└── README.md
app.py

Handles the Streamlit user interface, conversation management, PDF uploads, streaming responses, and human-in-the-loop interactions.

backend.py

Contains the LangGraph agent workflow, Gemini integration, RAG pipeline, vector retrieval, tool definitions, conversation checkpointing, and agent execution logic.

🚀 Getting Started
1. Clone the repository
git clone https://github.com/Raj2531/Nexora-AI.git
cd Nexora-AI
2. Create a virtual environment
python -m venv venv

Activate it:

Windows

venv\Scripts\activate

macOS / Linux

source venv/bin/activate
3. Install dependencies
pip install -r requirements.txt
4. Configure environment variables

Create a .env file:

GOOGLE_API_KEY=your_google_api_key
TAVILY_API_KEY=your_tavily_api_key
OPENWEATHER_API_KEY=your_openweather_api_key

Add any additional credentials required by the enabled tools.

Never commit your .env file or API keys to GitHub.

5. Run the application
streamlit run app.py

The application will be available locally at:

http://localhost:8501
🐳 Running with Docker

Build the Docker image:

docker build -t nexora-ai .

Run the container:

docker run -p 8501:8501 --env-file .env nexora-ai

Open:

http://localhost:8501
🔐 Security

Nexora AI uses environment-based configuration for API credentials.

Recommended production practices include:

Never committing API keys
Using GitHub Actions Secrets for CI/CD credentials
Restricting API permissions
Applying rate limits to external APIs
Validating tool inputs
Using secure secret-management solutions in production
🔮 Future Improvements
 PostgreSQL + pgvector for persistent vector storage
 React-based production frontend
 REST API backend
 JWT authentication
 Redis-based caching
 Advanced agent routing
 LangSmith observability and tracing
 Google Cloud Run deployment
 Automated evaluation of RAG responses
 Retrieval quality and latency monitoring
 Enterprise knowledge-base connectors
📌 Use Cases

Nexora AI can be extended for:

Enterprise knowledge assistants
Customer support automation
Document intelligence
Internal knowledge search
Research assistants
AI-powered workflow automation
Tool-using enterprise agents
