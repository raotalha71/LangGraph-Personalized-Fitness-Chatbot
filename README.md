# LangGraph Personalized Fitness Chatbot

README: LangGraph Personalized Fitness Chatbot
Overview
This script (langgraph_fitness_chatbot.py) implements a Personalized Fitness Chatbot using LangGraph with the Grok API (Llama-3.3-70B-Versatile model). It provides tailored fitness advice (e.g., "I want to run a marathon") with persistent memory across sessions, using memory management and RAG.
Features

Scenario: Tracking user fitness goals in a fitness app.
Memory Management:
Short-Term Memory (STM): Checkpointer (in-memory) for conversation state.
Long-Term Memory (LTM): Pinecone for user goal embeddings.
RAG: Retrieves goals from Pinecone, with history trimmed to ~1000 tokens.


Tools: Grok API, HuggingFaceEmbedding (sentence-transformers/all-MiniLM-L6-v2), Pinecone, LangGraph components (StateGraph, Checkpointer).

Setup
Prerequisites

Python 3.8+ (recommended).
Grok API key (Grok console).
Pinecone API key (Pinecone).
Google Colab or local Python environment.

Installation

Install dependencies:pip install pinecone==7.0.2 langchain langchain-groq langgraph sentence-transformers


Set environment variables:
Replace your_grok_api_key_here with your Grok API key.
Replace your_pinecone_api_key_here with your Pinecone API key.



Data Preparation

The script includes a sample fitness goal in Pinecone ("Run a marathon in 6 months").
Add or modify goals by updating the fitness_index.upsert() call.

Usage

Save the script as langgraph_fitness_chatbot.py.
Run the script in Colab or a local environment:python langgraph_fitness_chatbot.py


Observe the console output for the response to the query: "I want to run a marathon."
Test with custom queries by modifying the app.invoke() input.
Visualize the workflow using the Mermaid diagram (below) in Mermaid Live Editor.

Mermaid Workflow Diagram
graph TD
    A[User Query] --> B[Checkpointer: STM]
    B --> C[RAG: Pinecone Goals]
    C --> D[Generate Response]
    D --> E[Response]

Memory Management

STM: Checkpointer tracks conversation state (query, history) within a session.
LTM: Pinecone stores goal embeddings for cross-session persistence.
RAG: Retrieves relevant goals from Pinecone, with history trimmed to ~1000 tokens for efficiency.

Pros and Cons

Pros:
Highly customizable workflow.
Flexible memory management.


Cons:
Requires expertise to design graphs.
Pinecone dependency adds external cost.
