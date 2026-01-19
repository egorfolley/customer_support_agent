# Customer Support Agent

![1768799221408](images/arch.png)

# **THE INITIAL JUPYTER CODE - work in progress**

## Overview

This project is a **Customer Support AI Agent** designed to help teams process and triage incoming customer complaints efficiently. The system ingests customer emails (provided as PDFs), analyzes their content, classifies them by urgency and topic, and generates **internal fix instructions** to guide human operators in resolving issues.

The solution is built as an **agentic RAG (Retrieval-Augmented Generation) pipeline** with human-in-the-loop (HITL) control, making it suitable for internal operations, customer support, and executive oversight.

## Problem

Organizations receive a high volume of customer complaints across multiple domains (e.g., billing, outages, product issues). These requests are often:

* Unstructured (free-form emails)
* Time-sensitive (varying urgency levels)
* Repetitive (similar issues reoccur over time)

Manually reviewing, prioritizing, and diagnosing each request is time-consuming and does not scale.

## Solution

This project introduces an **AI-powered internal support agent** that:

* Extracts and parses customer complaint emails from PDFs
* Classifies requests by urgency (P1 / P2 / P3) and topic
* Stores structured metadata in a relational database and semantic embeddings in a vector database
* Uses agentic RAG to:
  * Diagnose the underlying problem
  * Identify likely root causes using historical context
  * Generate **clear, actionable fix instructions** for human operators

The system does **not** auto-resolve issues or respond directly to customers. All outputs are designed for  **human review and execution**

## Architecture Highlights

* **Input Processing:** Email PDFs → text extraction → structured parsing
* **LLM Classification:** Urgency, topic, and keyword extraction
* **Storage:**
  * Relational DB (SQLite / PostgreSQL) for raw data and metadata
  * Vector DB (Milvus) for semantic retrieval
* **Agentic Workflow:**
  * Tool-based agent orchestration
  * Retrieval-augmented diagnosis
  * Prescriptive fix plan generation
* **Safety:** Human-in-the-loop by design

## Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Set up environment variables in [.env](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) (e.g., API keys for Grok)
3. Run the notebook cells to load data, classify emails, store in DBs, and execute the agent

## Usage

Typical workflow:

1. Load an email provided as a PDF
2. Classify the email by urgency and topic
3. Store structured data and embeddings
4. Invoke the agent with the email context
5. Receive a JSON output containing:
   * Problem statement
   * Likely root causes
   * Recommended internal actions
   * Ownership and escalation signals

All outputs are intended for internal teams and decision-makers.

## Roadmap / TODO

* [ ] Integrate codebase analysis for deeper technical context (RAG over repositories)
* [ ] Build a backend API using FastAPI for email ingestion and agent invocation
* [ ] Develop a frontend UI (e.g., React) for uploading emails and reviewing results
* [ ] Add feedback loops to learn from resolved cases
* [ ] Integrate ticketing systems (e.g., Jira, Linear)
