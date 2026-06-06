<div align="center">
  <img src="frontend/public/app_logo.png" alt="Cognivio AI" width="160" />

  # Cognivio AI

  **AI-Powered Learning Platform — Turn Any Document Into an Interactive Study Experience**

  [![Status](https://img.shields.io/badge/Status-Live-brightgreen?style=flat-square)](#)
  [![Platform](https://img.shields.io/badge/Platform-Web-blue?style=flat-square)](#)
  [![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](#license)

  [Visit Cognivio AI →](#) · [View Demo →](#)

</div>

---

## What is Cognivio AI?

Cognivio AI is a full-stack SaaS platform that transforms static documents into rich, interactive learning experiences — powered by AI. Upload any study material and instantly generate summaries, flashcards, quizzes, audio overviews, podcast-style explanations, video recaps, and more.

Designed for students, self-learners, and professionals who want to absorb information faster and retain it longer.

---

## ✨ Key Features

| Feature | Description |
|---|---|
| **📄 Smart Document Library** | Upload, organize, and manage study materials in a centralized workspace |
| **🧠 AI Summaries** | Instantly distill long documents into concise, structured summaries |
| **🗂️ Flashcard Generation** | Auto-generate flashcards with smart review tracking and starred cards |
| **📝 Quiz Engine** | AI-generated quizzes with scoring, detailed results, and performance insights |
| **💬 Contextual AI Chat** | Ask follow-up questions and get document-aware, conversational answers |
| **🎙️ Voice Chat** | Real-time voice conversations with an AI tutor that understands your documents |
| **🔊 Voice Overview** | One-click audio summaries for on-the-go revision |
| **🎧 Podcast Overview** | Long-form, podcast-style deep dives into your study material |
| **🎬 Video Overview** | AI-generated video recaps combining visual and verbal explanations |
| **💡 Concept Explainer** | Break down complex topics into clear, learner-friendly explanations |
| **📊 Learning Dashboard** | Track study activity, progress, and performance across all content |
| **💳 Subscription Billing** | Tiered plans (Free / Plus / Pro / Premium) with seamless checkout |

---

## 🏗️ Architecture Overview

Cognivio AI is built as a modern, decoupled SaaS application with a clear separation between the client and server:

```
┌─────────────────────────┐       REST API       ┌─────────────────────────┐
│                         │ ◄──────────────────►  │                         │
│     Next.js Frontend    │                       │   Express.js Backend    │
│     (React 19 / TS)     │                       │   (Node.js API)         │
│                         │                       │                         │
└────────────┬────────────┘                       └────────────┬────────────┘
             │                                                 │
             │                                    ┌────────────┴────────────┐
             │                                    │                         │
             │                                    │     MongoDB Atlas       │
             │                                    │     (Data Layer)        │
             │                                    │                         │
             │                                    └─────────────────────────┘
             │
    ┌────────┴─────────────────────────────────────────────────┐
    │                    Third-Party Services                   │
    │                                                          │
    │  Google Gemini · ElevenLabs · Vapi · Cloudinary          │
    │  LemonSqueezy · Google OAuth · Nodemailer                │
    └──────────────────────────────────────────────────────────┘
```

### Frontend

- **Next.js 16** with App Router and React 19
- **TypeScript** for type safety across the entire codebase
- **Tailwind CSS 4** + **Radix UI** for a polished, accessible component system
- **Framer Motion** for smooth animations and micro-interactions
- Modular service layer for clean API communication

### Backend

- **Express 5** REST API with modular controller/route architecture
- **MongoDB** with Mongoose ODM for flexible data modeling
- **JWT + Google OAuth** authentication with secure session management
- Production-grade security: Helmet, HPP, CORS, rate limiting
- **AI Pipeline**: Google Gemini for content generation, ElevenLabs for voice synthesis, Puppeteer + FFmpeg for video rendering
- **LemonSqueezy** integration for subscription lifecycle and webhook processing

---

## 🔐 Security & Infrastructure

- **Authentication**: Email/password with OTP verification + Google OAuth
- **Authorization**: JWT-based protected API layer
- **Data Security**: Encrypted credentials, secure cookie-based sessions
- **API Protection**: Rate limiting, CORS enforcement, input validation (Joi)
- **Media Pipeline**: Cloudinary CDN for asset delivery, server-side media processing
- **Payments**: PCI-compliant billing via LemonSqueezy with webhook verification

---

## 🎯 Engineering Highlights

- **Full-Stack TypeScript/JavaScript** — Unified language across frontend and backend
- **AI-First Architecture** — Deep integration with multiple AI providers for content generation, voice synthesis, and video creation
- **Real-Time Voice AI** — Live conversational learning powered by Vapi workflow orchestration
- **Automated Media Pipeline** — Server-side audio/video generation using ElevenLabs, Puppeteer, and FFmpeg
- **Production-Ready SaaS** — Complete subscription billing, user management, and webhook infrastructure
- **Modular Codebase** — Clean separation of concerns with dedicated controllers, services, models, and middleware layers
- **Responsive & Accessible** — Mobile-first design with Radix UI primitives and WCAG-conscious component patterns

---

## 📈 Product Tiers

| Plan | Features |
|---|---|
| **Free** | Limited document uploads, basic AI summaries |
| **Plus** | Extended uploads, flashcards, quizzes |
| **Pro** | Full access including voice/podcast/video overviews |
| **Premium** | Unlimited usage across all features |

---

## 🛠️ Tech Stack at a Glance

| Layer | Technologies |
|---|---|
| **Frontend** | Next.js 16, React 19, TypeScript, Tailwind CSS 4, Radix UI, Framer Motion |
| **Backend** | Node.js, Express 5, MongoDB, Mongoose, JWT, Passport |
| **AI & Media** | Google Gemini, ElevenLabs, Vapi, Puppeteer, FFmpeg |
| **Infrastructure** | Cloudinary, LemonSqueezy, Nodemailer, Google OAuth |

---

## 📂 Repository Structure

This project is organized as a monorepo with Git submodules:

```
CognivioAI/
├── frontend/          → Next.js client application
├── server/            → Express.js API server
└── README.md          → You are here
```

Each submodule has its own dedicated README with additional details about its architecture and responsibilities.

---

## License

This is proprietary software. All rights reserved.

This codebase is **not open source** and is not licensed for redistribution, modification, or commercial use. The source code is published for portfolio and demonstration purposes only.

© 2025 Cognivio AI. All rights reserved.
