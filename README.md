# Multi-Agent System Lab Exercise

This lab demonstrates how to build a customer support system using sub agents that are deployed using Studio or LangSmith Deployments using LangGraph's multi-agent architecture. The system features a **supervisor agent** that intelligently delegates tasks to specialized **subagents** for handling music catalog and invoice queries.

This example was adapted from the multiagent workbook found here: https://github.com/langchain-ai/langgraph-101/blob/main/notebooks/201/multi_agent.ipynb

## Overview

The project includes:
- **Supervisor Agent**: Routes customer queries to appropriate subagents
- **Music Catalog Subagent**: Handles queries about songs, albums, and artists
- **Invoice Information Subagent**: Retrieves customer purchase history and invoice details
- **Comprehensive Evaluation**: Tests routing accuracy, invoice sub agent, and end-to-end supervisor agent

## Prerequisites

- Python 3.11+
- [uv](https://docs.astral.sh/uv/) package manager
- LangGraph CLI
- API keys for Anthropic (or OpenAI)

## Setup Instructions

1. **Install dependencies**
   ```bash
   uv sync
   ```

2. **Configure environment variables**

   Create a `.env` file in the project root with your API keys:
   ```
   ANTHROPIC_API_KEY=your_anthropic_key_here
   LANGSMITH_API_KEY=your_langsmith_key_here
   LANGSMITH_TRACING="true"
   LANGSMITH_PROJECT="langgraph-101"
   ```

3. **Start the LangGraph development server**
   ```bash
   uv run langgraph dev --allow-blocking
   ```

   This will:
   - Start the LangGraph Studio on `http://localhost:2024`
   - Launch both subagent graphs defined in your `langgraph.json`
   - Enable the supervisor to communicate with remote subagents

## Running the Lab

1. **Open the notebook**

   Launch Jupyter and open `multi_agent_sdk.ipynb`

2. **Follow the lab exercises**

   The notebook walks you through:
   - Setting up the multi-agent system
   - Creating the supervisor agent
   - Connecting to remote subagents
   - Testing the complete system
   - Evaluating performance at multiple levels

3. **View traces in LangSmith**

   With `distributed_tracing=True`, you can see nested execution traces in LangSmith for debugging and analysis.

## Project Structure

```
.
├── agents/                    # Individual agent implementations
├── utils/                     # Helper utilities
├── multi_agent_sdk.ipynb     # Main lab notebook
├── langgraph.json            # LangGraph server configuration
├── dataset_*.jsonl           # Evaluation datasets
└── README.md                 # This file
```

## Evaluation Strategy

The lab includes four levels of evaluation:

1. **Routing Accuracy**: Verify the supervisor routes to the correct subagent
2. **Response Quality**: Use LLM-as-judge to assess answer correctness
3. **Subagent Performance**: Test individual subagents in isolation
4. **End-to-End Testing**: Validate the complete user journey


## Resources

- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [LangSmith Documentation](https://docs.smith.langchain.com/)
- [LangGraph SDK Documentation](https://langchain-ai.github.io/langgraph/cloud/reference/sdk/python_sdk_ref/)
