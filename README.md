# Elastic-Agent-Builder-Hackathon-SLEUTH-Archivist
A self-improving agent architecture combining n8n and Elastic MCP. By implementing a "Strict Evidence Check" and a "Human-in-the-Loop" workflow, it eliminates hallucinations in RAG systems caused by evidence sparsity.

# 🏛️ SLEUTH-Archivist: Self-Improving Agentic RAG for Cultural Heritage

[![Hackathon](https://img.shields.io/badge/Elasticsearch-Agent%20Builder%20Hackathon-blue)](https://elasticsearch.devpost.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

![The Demo]

<img width="2560" height="1332" alt="Hero" src="https://github.com/user-attachments/assets/450fc51a-5366-4dee-8fc8-9bc2c6b623f7" />


## 💡 Overview
SLEUTH-Archivist is a specialized AI archivist built for the **National Museum of Taiwan History (NMTH)**. It addresses the critical issue of **"Evidence Sparsity"** (inspired by the SLEUTH framework) in traditional RAG systems. 

By implementing an **Agentic Context Engineering (ACE)** loop powered by **n8n** and **Elasticsearch MCP**, our system transitions from a static RAG to a self-improving expert system. It doesn't just "search"; it **reasons, identifies gaps, and learns from Human-in-the-Loop (HITL) feedback.**

## 🚀 Technical Highlights
* **Anti-Hallucination Protocol**: Implements a strict `evidence_check` via Kibana MCP. If quantitative facts are missing, the agent triggers a `knowledge_gap` status instead of hallucinating.
* **Early Experience (EE) Learning**: Treats historical QA logs (`nmth-qa-logs`) as a "World Model" for the agent to understand past failures and refine its search strategy.
* **Context Engineering**: Uses n8n to perform **Query Transformation**, ensuring complex historical queries are correctly mapped to Elasticsearch vector space.

## 🛠️ Architecture
Our multi-agent system orchestrates reasoning and retrieval through a unified MCP layer:

```mermaid
graph TD
    User((User Query)) --> Router[n8n Router & Query Rewriter]
    Router --> Agent[Elastic Agent Builder / MCP]
    Agent --> Search{Search Tools}
    Search --> KB[(NMTH Knowledge Base)]
    Search --> Logs[(QA Experience Logs)]
    Agent -- "Evidence Found" --> Final[Response with Citations]
    Agent -- "Evidence Missing" --> HITL[Human-in-the-Loop / Curator]
    HITL -- "Inject Fact" --> KB

```

![Elasticsearch: Index]

<img width="798" height="427" alt="two-indexes" src="https://github.com/user-attachments/assets/0e2fc904-1e12-4c3d-8edf-d18160bf5e49" />
<img width="1072" height="515" alt="knowledge-base-index" src="https://github.com/user-attachments/assets/5d4bed37-c286-4787-a7f8-193abbd246e2" />
<img width="1172" height="1101" alt="qa-logs-index" src="https://github.com/user-attachments/assets/9e297a19-4541-4784-aa80-e50b48223772" />


![Elasticsearch: Tools]

<img width="1247" height="1126" alt="tools" src="https://github.com/user-attachments/assets/fcd510c6-ad93-413d-a9ee-5ce2002f209b" />


![n8n]

<img width="1527" height="871" alt="n8n" src="https://github.com/user-attachments/assets/d6ee5e59-8f1a-4558-b2eb-902903be840e" />



## 🎬 Demo Scenario: The Self-Improving Loop

1. **The Gap**: A user asks for "17th-century VOC map preservation standards". The Agent detects missing facts and returns a structured `{"status": "knowledge_gap"}`.
2. **The Expert (Human in The Loop)**: The museum curator reviews gap logs and injects the official standard (20°C / 50% RH) into Elasticsearch.
3. **The Evolution**: Upon the next identical query, the Agent retrieves the newly available context, fulfilling the **ACE loop** to provide a hallucination-free answer.

## 📦 Setup & Deployment

1. **Prerequisites**:
* Elastic Cloud deployment
* n8n instance (with AI Agent node support)


2. **Environment Variables**:
* Copy `.env.example` to `.env` and fill in your `ELASTIC_API_KEY` and `MCP_SERVER_URL`.


3. **Import Workflow**:
* Download `workflows/sleuth-archivist-v1.json` and import it into your n8n.



---

### 🎥 Video Demo & Social

* **Watch the Demo**: [🔗 https://youtu.be/rfEJS_rWBTw]
* **Social Post**: [🔗 Link to X/LinkedIn Post tagged @elastic_devs]

```
