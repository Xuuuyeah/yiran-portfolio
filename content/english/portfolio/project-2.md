---
title: "Agentic AI Analytics Platform"
date: 2025-07-01T12:00:00+00:00
image: "images/portfolio/item2.jpg"
categories: ["ai-agent","data-science"]
description: "Multi-agent LLM system with LangGraph orchestration for end-to-end natural language data analytics."
draft: false
external_url: "/architecture_diagram.html"
project_info:
- name: "Tech Stack"
  icon: "fas fa-layer-group"
  content: "Python, LangGraph, LangChain, Azure OpenAI GPT-4, MCP, Snowflake, Plotly, Streamlit, Pandas"
- name: "Architecture"
  icon: "fas fa-project-diagram"
  content: "Multi-Agent Supervisor Pattern (LangGraph StateGraph)"
- name: "Domain"
  icon: "fas fa-robot"
  content: "Agentic AI & Data Analytics"
---

Designed and implemented a production multi-agent LLM system that enables end-to-end natural language data analytics — from user query to actionable insight — powered by LangGraph orchestration and Azure OpenAI GPT-4.

#### Architecture Overview

Built a **Supervisor Agent** pattern using LangGraph's `StateGraph` that dynamically routes tasks to **5 specialized ReAct agents** via `Command(goto=[Send(agent_name, input)])`:

- **Snowflake Agent** — Queries enterprise data warehouse through MCP (Model Context Protocol) with `SQLWriteDetector` safety guard
- **Visualizer Agent** — Generates interactive Plotly charts (graph_objects, express, plotly.io → HTML)
- **Python Interpreter Agent** — Executes sandboxed code with AST security guard blocking unsafe operations
- **Flowchart Agent** — Produces Mermaid diagrams from code analysis via `read_code_file()`
- **CSV Export Agent** — Transforms and exports data as CSV/Excel/JSON via Pandas

#### Key Technical Highlights

- **LangGraph StateGraph** with typed `Command` routing enables dynamic multi-step pipelines (e.g., query → analyze → visualize → export)
- **MCP Protocol** decouples Snowflake access as a stdio MCP server, with `MultiServerMCPClient` and schema-aware NL→SQL generation
- **Human-in-the-Loop** via `interrupt()` mechanism for supervisor to request human guidance mid-pipeline
- **MemorySaver** checkpointing enables session persistence across multi-agent conversations
- **Streamlit Web UI** with asyncio bridge for real-time token streaming from LangGraph's async runtime
- **Zero-install deployment** via UV portable bundle — auto-provisions Python + all dependencies on any Windows machine
