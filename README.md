<div align="center">
  <img src="frontend/public/app_logo.png" alt="Cognivio AI" width="160" />

  # Cognivio AI

  **AI-Powered Learning Platform — Turn Any Document Into an Interactive Study Experience**

  [![Status](https://img.shields.io/badge/Status-Live-brightgreen?style=flat-square)](#)
  [![Platform](https://img.shields.io/badge/Platform-Web-blue?style=flat-square)](#)
  [![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](#license)
</div>

---

## What is Cognivio AI?

Cognivio AI is a full-stack SaaS platform that transforms static documents into rich, interactive learning experiences — powered by AI. Upload any study material and instantly generate summaries, flashcards, quizzes, audio overviews, podcast-style explanations, video recaps, and more.

---

## 🏗️ System Architecture

Cognivio AI is built as a modern, decoupled SaaS application. The frontend is a Next.js 16 application running React 19, communicating via REST API with a Node.js/Express backend. 

### High-Level Architecture Diagram

```mermaid
graph TD
    Client[Next.js Client Area<br>React 19 / Tailwind 4]
    API[Express.js API Server<br>Node.js]
    DB[(MongoDB Atlas<br>Vector Store / User Data)]
    
    Client <-->|REST API / JSON| API
    API <-->|Mongoose / Langchain| DB
    
    subgraph Third-Party AI & Media Services
        Gemini[Google Gemini / LLMs]
        ElevenLabs[ElevenLabs Voice API]
        Remotion[Remotion / Puppeteer Video Rendering]
        Cloudinary[Cloudinary CDN]
        Vapi[Vapi Real-time Voice]
    end
    
    API <-->|Text/Prompts| Gemini
    API <-->|Text-to-Speech| ElevenLabs
    API <-->|Render Video| Remotion
    API <-->|Upload Media| Cloudinary
    Client <-->|WebRTC Voice Chat| Vapi
```

---

## 🛠️ Complete Tech Stack

### Frontend (Client)
- **Framework**: Next.js 16 (App Router)
- **UI Library**: React 19
- **Language**: TypeScript
- **Styling**: Tailwind CSS 4, Radix UI, framer-motion, clsx, tailwind-merge
- **State & Data Handling**: react-hook-form, axios
- **Markdown & Math**: react-markdown, remark-gfm, remark-math, rehype-katex, katex
- **PDF Rendering**: react-pdf
- **Authentication**: @react-oauth/google, jwt-decode
- **Payments**: @paddle/paddle-js
- **Voice Agent**: @vapi-ai/web

### Backend (Server)
- **Core**: Node.js, Express 5
- **Language**: TypeScript
- **Database**: MongoDB with Mongoose ODM
- **AI & RAG Pipeline**: 
  - @google/genai, @google/generative-ai, openai
  - langchain, @langchain/mongodb, @langchain/textsplitters
  - @llamaindex/llama-cloud
- **Video & Audio Generation**:
  - remotion, @remotion/renderer, @remotion/bundler
  - @elevenlabs/elevenlabs-js
  - puppeteer, puppeteer-extra, puppeteer-screen-recorder
  - fluent-ffmpeg
- **Document Parsing & File Processing**: LlamaParse (@llamaindex/llama-cloud), multer, cloudinary, pdf-parse
- **Security & Auth**: passport, passport-google-oauth20, bcryptjs, jsonwebtoken, helmet, express-rate-limit, express-mongo-sanitize, hpp
- **Payments & Emails**: @paddle/paddle-node-sdk, @lemonsqueezy/lemonsqueezy.js, resend

---

## ⚙️ Core Processing Flows

### 1. Document Processing & RAG (Retrieval-Augmented Generation)

When a user uploads a PDF or document, the system orchestrates a pipeline to parse, chunk, embed, and store the text for contextual AI queries.

```mermaid
sequenceDiagram
    participant U as User
    participant C as Next.js Client
    participant A as Express API
    participant LP as LlamaParse
    participant LC as LangChain/TextSplitter
    participant G as Gemini Embeddings
    participant DB as MongoDB Vector Store

    U->>C: Upload PDF / Document
    C->>A: POST /api/documents (File)
    A->>LP: Extract Text & Structure (LlamaParse API)
    LP-->>A: Parsed Markdown / Text
    A->>LC: Chunk text (RecursiveCharacterTextSplitter)
    LC->>G: Request Embeddings for chunks
    G-->>LC: Return Vector Embeddings
    LC->>DB: Store chunks & vectors (Atlas Vector Search)
    A-->>C: Document Processed Successfully
```

**Chatting with Documents (Contextual Q&A)**:
When the user asks a question, the query is embedded, matched against the vector store to fetch relevant chunks, and sent to the LLM (Gemini) alongside the user's prompt to generate a grounded answer.

### 2. Quiz & Flashcard Generation

The AI autonomously creates study materials from the extracted document context.

```mermaid
flowchart LR
    Doc[Document Text Chunks] --> Prompt[System Prompt:<br>'Generate 10 MCQs and Flashcards']
    Prompt --> LLM[Google Gemini LLM]
    LLM --> JSON[Structured JSON Output<br>Q&A Pairs]
    JSON --> DB[(MongoDB<br>Quizzes & Flashcards)]
    DB --> Client[Frontend UI<br>Interactive Study Mode]
```

### 3. Video Overview Generation

One of the most advanced features is generating complete, narrated video recaps of documents entirely on the backend.

```mermaid
sequenceDiagram
    participant C as Client
    participant A as Express API
    participant G as Gemini
    participant E as ElevenLabs
    participant R as Remotion / Puppeteer
    participant CDN as Cloudinary

    C->>A: Request Video Overview
    A->>G: Generate Video Script & Visual Prompts from Document
    G-->>A: JSON Script (Dialogue + Visual Cues)
    A->>E: Convert Dialogue to Speech (TTS)
    E-->>A: Audio File (.mp3)
    A->>R: Trigger Headless Browser Render<br>(Inject Audio + Visuals via Remotion)
    R-->>A: Rendered Video (.mp4)
    A->>CDN: Upload Video File
    CDN-->>A: Video URL
    A-->>C: Return Video URL & Save to User Profile
```

### 4. Real-time Voice Chat (AI Tutor)

Users can have conversational voice calls with the AI about their documents.

```mermaid
graph TD
    User((User)) <-->|WebRTC Audio| Vapi[Vapi.ai Voice Orchestrator]
    Vapi <-->|Function Calling / Context| API[Cognivio Backend API]
    API <-->|Fetch RAG Context| DB[(MongoDB Vector Store)]
```

---

## 🔐 Security & Authentication

- **User Auth**: JWT-based authentication combined with Google OAuth 2.0 (via Passport).
- **Session Protection**: Rate limiting, HTTP Parameter Pollution (HPP) protection, MongoDB Query Sanitization, and Helmet for secure headers.
- **Validation**: Strict input validation using Zod and Joi.


## License

This is proprietary software. All rights reserved.

This codebase is **not open source** and is not licensed for redistribution, modification, or commercial use. The source code is published for portfolio and demonstration purposes only.

© 2026 Cognivio AI. All rights reserved.
