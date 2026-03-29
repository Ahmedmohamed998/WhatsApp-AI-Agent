# WhatsApp AI Agent

> High-converting, multi-lingual WhatsApp AI sales agent built for the Mermates Diving Team.

## Overview

An aggressive, conversion-optimized WhatsApp AI assistant designed to close diving course bookings natively. Using an advanced Retrieval-Augmented Generation (RAG) backend and covert multi-lingual Voice AI processing, the persona ("Dana") intelligently guides customers entirely from initial inquiry to paid reservations without human intervention.

---

## Features

- **Conversational Sales Funnel** — Acts as a confident, human-like sales representative. Uses strict step-by-step qualification strategies (Greeting ➔ Qualification ➔ Soft Close ➔ Payment Link) to drive actual revenue, not just informal chatter.
- **Advanced Multilingual Voice AI (Hidden Feature)** — Capable of ingesting native WhatsApp customer voice notes, transcribing them, understanding the core intent, and responding with hyper-realistic AI-generated voice recordings in multiple languages (acoustically indistinguishable from a real human agent).
- **Intelligent RAG & Contextual Vector Search** — Utilizes `Cohere` multilingual embeddings (v3.0) and `Pinecone` to instantly retrieve accurate pricing, diving course details, and designated payment links. Hallucinations of payment URLs and policies are strictly bounded.
- **Robust Prompt Bounding & Cleansing** — Custom regex and parsing pipelines proactively strip out all LLM-generated markdown, asterisks, and logic artifacts to ensure a native, plain-text WhatsApp messaging experience.
- **Full-stack Management Dashboard** — Built with Next.js and Prisma, providing administrators with real-time oversight of WhatsApp conversations, intent tracking, and automated CRM logging.

---

## Architecture

```text
      Customer (Text / Voice Notes)
               │
    Next.js + WhatsApp Webhooks
   ┌───────────┴───────────────┐
   │ 1. Voice-to-Text ASR      │
   │ 2. Intent Validation      │
   │ 3. Forward to RAG Engine  │
   └───────────┬───────────────┘
               │
      FastAPI Microservice
   ┌───────────┴───────────────┐
   │ 1. Cohere Embeddings      │
   │ 2. Pinecone DB Lookup     │
   │ 3. Azure OpenAI Inference │
   │ 4. Text-to-Voice Neural   │
   └───────────┬───────────────┘
               │
     WhatsApp Audio/Text Reply
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **AI Inference & Voice** | Azure OpenAI (GPT-5.2-chat), Advanced TTS/ASR Pipelines |
| **Embeddings & Vector Store**| Cohere (embed-multilingual-v3.0), Pinecone |
| **Backend Microservice**| FastAPI (Python) |
| **Fullstack Dashboard** | Next.js 16, React, Tailwind CSS |
| **Database & ORM** | PostgreSQL, Prisma ORM |

---

## Core AI & Sales Pipelines

### 1. Conversion-Obsessed Prompt Engineering
The core logic relies on an intricate, multi-stage sales prompt acting as a state machine. The agent restricts itself to asking only one question at a time to avoid overwhelming the user. It naturally progresses through a warm greeting, capability alignment (e.g., beginner trial vs. PADI certified), transparent pricing delivery, and forcefully triggers "soft closes" by requesting preferred dates and party sizes.

### 2. Multi-Lingual Voice Synthesis Integration
Deployed in production environments, the architecture securely intercepts native WhatsApp `.ogg` voice notes. It passes them through a sophisticated Automatic Speech Recognition (ASR) layer, processes the textual intent via the RAG pipeline, and renders the reply through neural Text-to-Speech (TTS) engines. The resulting audio mimics localized dialects, providing an unparalleled, humanized customer retention experience.

### 3. Hyper-Accurate Payment Link Retrieval
To mitigate the severe risks of an LLM inventing fake payment gateways or unauthorized discounts, the prompt enforces a strict operational protocol where payment URLs must be explicitly retrieved from the Pinecone Vector Database index. If a trusted link isn't found within two retrieval attempts, the AI safely degrades to a manual WhatsApp handover link for a human agent to intercept.

---

## License

Private — all rights reserved. Built specifically for Transformix / Mermates. This document serves purely as a high-level architectural overview for portfolio showcase purposes.
