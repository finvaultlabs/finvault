# 🛡️ Finvault: Air-Gapped AI Coding Assistant

![Status](https://img.shields.io/badge/Status-Proof_of_Concept-orange)
![Environment](https://img.shields.io/badge/Environment-Air--Gapped_Financial_Network-red)
![Middleware](https://img.shields.io/badge/Middleware-JBoss_EAP-blue)
![VectorDB](https://img.shields.io/badge/VectorDB-ChromaDB-10b981)
![AI](https://img.shields.io/badge/AI-Ollama-black)
![Model](https://img.shields.io/badge/Model-DeepSeek_Coder_6.7b-purple)

---

## 📌 The Problem
In strict financial and enterprise environments, connecting to cloud-based LLMs (like OpenAI or Claude) is strictly prohibited due to **data privacy and air-gapped network policies**.
How can developers leverage the power of AI coding assistants without sending a single byte of confidential codebase to the outside world?

---

## 💡 The Solution
Finvault is a reference architecture and deployment guide for running a **100% offline, locally hosted AI coding assistant**.
By combining **Ollama** (for local LLMs), **ChromaDB** (for RAG), and enterprise middleware (**JBoss EAP**), this project delivers intelligent code generation with complete data sovereignty.

> **No internet. No data leaks. Complete control.**

---

## 🏗️ Architecture Overview

```mermaid
graph TD
    subgraph Air-Gapped Financial Network
        Client[Developer / IDE] -->|HTTP/HTTPS| JBoss[JBoss EAP Server]

        subgraph Finvault Core
            JBoss -->|Retrieval| Chroma[(ChromaDB\nVector Storage)]
            JBoss -->|Prompt + Context| Ollama[Ollama LLM Engine]
        end

        Ollama -->|Loads Model| LocalWeights[(Local Weights\nDeepSeek Coder 6.7b)]
    end

    External[External Internet] -.-|BLOCKED BY FIREWALL| JBoss
    External -.-|BLOCKED BY FIREWALL| Ollama

    style External stroke:#f66,stroke-width:2px,stroke-dasharray: 5 5
    style JBoss fill:#0066cc,color:#fff
    style Ollama fill:#000,color:#fff
    style Chroma fill:#10b981,color:#fff
    style LocalWeights fill:#7c3aed,color:#fff
