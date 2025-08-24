# LangChain AI Research Agent - Project Structure

## Overview
Professional LangChain-based AI Research Agent with Gemini 2.5 Flash integration.

## Project Structure

```
langchain-research-agent/
├── main.py                     # Main interactive application
├── fastapi_app.py             # FastAPI web API with background tasks
├── test_fastapi.py            # FastAPI testing script
├── config.py                   # Configuration settings (loads from .env)
├── .env                        # Environment variables (API keys)
├── .gitignore                  # Git ignore file (protects .env)
├── requirements.txt            # Python dependencies
├── unit_test.py               # Unit tests
├── README.md                   # Project documentation
├── FASTAPI_README.md          # FastAPI-specific documentation
├── CONFIGURATION.md           # Configuration guide
├── PROJECT_STRUCTURE.md        # This file
├── agents/
│   ├── __init__.py
│   └── research_agent.py       # Core LangChain agent implementation
├── memory/
│   ├── __init__.py
│   └── conversation_memory.py  # Memory management
├── data/                       # Data storage directory
└── reports/                    # Generated research reports
```

## Key Files

- **main.py**: Interactive command-line interface for the research agent
- **fastapi_app.py**: FastAPI web API with background task processing
- **test_fastapi.py**: Comprehensive API testing script
- **agents/research_agent.py**: Core LangChain agent with embedded tools (web search, calculator, file operations)
- **config.py**: Configuration management with environment variable loading
- **.env**: Environment variables for API keys (secure configuration)
- **memory/conversation_memory.py**: Conversation buffer memory management
- **CONFIGURATION.md**: Comprehensive configuration guide

## Usage

### CLI Interface
```bash
python main.py
```

### FastAPI Web API
```bash
python fastapi_app.py
```
Then access:
- **API Server**: http://localhost:8000
- **Interactive Docs**: http://localhost:8000/docs
- **Health Check**: http://localhost:8000/health

### API Testing
```bash
python test_fastapi.py
```

## Features

- ✅ Real-time web search and information retrieval
- ✅ Mathematical calculations and data analysis  
- ✅ Professional research report generation
- ✅ Conversation context and research continuity
- ✅ File management and data persistence

## Tools

The agent includes three embedded tools:
1. **Web Search** - Uses Gemini's native Google Search capability
2. **Calculator** - Performs mathematical calculations
3. **File Operations** - Creates and manages research reports

## Agent Framework

- **Framework**: LangChain with ReAct pattern
- **LLM**: Gemini 2.5 Flash  
- **Agent Type**: Zero-shot React Description
- **Memory**: Conversation Buffer Window