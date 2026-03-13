# Cognivio AI

A full-stack AI-powered learning platform that helps users convert documents into interactive study experiences.

The project combines a **Next.js frontend** with a **Node.js/Express backend** to support authentication, document processing, AI-generated learning content, and subscription billing.

It includes powerful learning features such as **Voice Chat**, **Voice Overview**, **Podcast Overview**, **Video Overview**, AI summaries, flashcards, quizzes, contextual chat, progress tracking, and subscription management for a complete SaaS learning workflow.

---

## Table of Contents

- [Overview](#overview)
- [Highlighted Features](#highlighted-features)
- [Core Features](#core-features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Available Scripts](#available-scripts)
- [API Surface (High-Level)](#api-surface-high-level)
- [Deployment Notes](#deployment-notes)
- [Troubleshooting](#troubleshooting)
- [Usage & License](#usage--license)

---

## Overview

Cognivio AI enables users to:

- Upload and manage learning documents
- Generate AI summaries, flashcards, and quizzes
- Ask contextual questions via chat
- Generate audio/video learning overviews
- Track learning progress from a dashboard
- Manage paid subscriptions via Paddle

The platform is designed for modular growth and separates UI concerns from API/business logic.

---

## Highlighted Features

- **Voice Chat**: Real-time conversational learning experience with document context.
- **Voice Overview**: One-click audio summary generation for quick revision.
- **Podcast Overview**: Long-form, podcast-style explanation for deeper learning.
- **Video Overview**: AI-generated video recap to combine visual and verbal explanation.
- **Document Upload & Library**: Upload, manage, and revisit study documents from a centralized workspace.
- **AI Summaries**: Instantly convert long documents into concise, structured summaries.
- **Flashcards**: Auto-generate flashcards and review them with progress-focused study flow.
- **Quizzes & Results**: Generate quizzes, submit answers, and review performance insights.
- **Contextual AI Chat**: Ask follow-up questions and get document-aware responses.
- **Concept Explainer**: Break down difficult topics into clear, learner-friendly explanations.
- **Learning Dashboard**: Track study activity and progress across content and assessments.
- **Authentication & Profiles**: Secure email/password + Google login with account management.
- **Subscription Billing**: Paddle-powered plans, checkout, and subscription lifecycle handling.

---

## Core Features

### Learning & AI
- Document upload and retrieval
- AI-powered summary generation
- Flashcard generation and review actions (including starred cards)
- Quiz generation, submission, and result retrieval
- Document-aware chat and concept explanation
- Voice chat with Vapi workflow integration
- Voice overview, podcast overview, and video overview generation

### User & Security
- Email/password authentication
- Google OAuth login
- JWT-based protected APIs
- Password reset flow via email
- Secure middleware stack: Helmet, HPP, CORS controls, and rate limiting

### Billing
- Plan-based subscriptions (free/plus/pro/premium)
- Paddle checkout and upgrade preview flows
- Paddle webhook handling for subscription lifecycle events

---

## Tech Stack

### Frontend
- Next.js 16 (App Router)
- React 19 + TypeScript
- Tailwind CSS 4
- Radix UI primitives
- Axios
- Framer Motion
- React Hook Form

### Backend
- Node.js + Express 5
- MongoDB + Mongoose
- JWT + Passport (Google OAuth strategy)
- Joi validation
- Nodemailer
- Multer + Cloudinary (file/media handling)

### AI & Media Integrations
- Google Gemini (`@google/genai`)
- ElevenLabs (voice generation)
- Vapi (voice workflow integration)
- Puppeteer-based automation/recording utilities
- FFmpeg-based media processing

### Payments
- Paddle (client + server SDKs)

---

## Architecture

- **Frontend (`frontend`)**: Next.js client application, route groups, reusable components, and service layer for API communication.
- **Backend (`server`)**: Express API with modular controllers/routes, MongoDB models, middleware, and third-party integrations.
- **Communication**: Frontend calls backend REST APIs using `NEXT_PUBLIC_API_URL`.

Default local ports typically used:
- Frontend: `3000`
- Backend: `8080` (recommended via `PORT` to avoid conflicts)

---

## Project Structure

```text
ai-learning-app/
├─ frontend/
│  ├─ src/
│  │  ├─ app/                 # Next.js App Router pages/layouts
│  │  ├─ components/          # Shared UI + feature tab components
│  │  ├─ services/            # Frontend API service wrappers
│  │  ├─ context/             # Auth and shared state context
│  │  ├─ lib/                 # Utility libs (e.g., Vapi setup)
│  │  └─ utils/               # API paths, axios instance, helpers
│  ├─ public/                 # Static assets
│  └─ package.json
│
├─ server/
│  ├─ config/                 # Cloudinary and environment-based configs
│  ├─ controllers/            # Request handlers (auth, AI, docs, billing, etc.)
│  ├─ database/               # MongoDB connection logic
│  ├─ middlewares/            # Auth and error middlewares
│  ├─ models/                 # Mongoose schemas
│  ├─ routes/                 # Express route modules
│  ├─ utils/                  # AI/media/payment/email helper utilities
│  ├─ uploads/                # Runtime upload directory (git-ignored)
│  ├─ index.js                # API server entrypoint
│  └─ package.json
│
└─ .gitignore                 # Root ignore rules
```

---

## Getting Started

### 1) Prerequisites

Install the following:

- Node.js 20+ (LTS recommended)
- npm 10+
- MongoDB instance (local or cloud)
- FFmpeg installed and available in PATH (required by media utilities)

### 2) Install dependencies

From the project root:

```bash
cd frontend && npm install
cd ../server && npm install
```

### 3) Configure environment variables

- Create `server/.env`
- Create `frontend/.env.local`

Use the templates below.

### 4) Run the backend

```bash
cd server
npm run dev
```

### 5) Run the frontend

```bash
cd frontend
npm run dev
```

Then open `http://localhost:3000`.

---

## Environment Variables

> Keep secrets in backend env files only. Never expose private API keys in frontend variables.

### Backend (`server/.env`)

```env
NODE_ENV=development
PORT=8080
CLIENT_URL=http://localhost:3000
MONGODB_URI=mongodb+srv://<user>:<pass>@<cluster>/<db>
JWT_SECRET=replace_with_strong_secret

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id

# AI Providers
GEMINI_API_KEY=your_gemini_key
ELEVEN_LABS_API_KEY=your_elevenlabs_key
GAMMA_API_KEY=your_gamma_key

# Email (password reset)
EMAIL_USER=your_email@example.com
EMAIL_PASS=your_email_password_or_app_password

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

# Paddle
PADDLE_API_KEY=your_paddle_api_key
PADDLE_WEBHOOK_SECRET=your_paddle_webhook_secret
PADDLE_PRICE_ID_PLUS=pri_xxx
PADDLE_PRICE_ID_PRO=pri_xxx
PADDLE_PRICE_ID_PREMIUM=pri_xxx

# Optional
MAX_CONCURRENT_RECORDINGS=1
```

### Frontend (`frontend/.env.local`)

```env
NEXT_PUBLIC_API_URL=http://localhost:8080
NEXT_PUBLIC_GOOGLE_CLIENT_ID=your_google_client_id
NEXT_PUBLIC_VAPI_PUBLIC_KEY=your_vapi_public_key
NEXT_PUBLIC_VAPI_WORKFLOW_ID=your_vapi_workflow_id
NEXT_PUBLIC_PADDLE_ENV=sandbox
NEXT_PUBLIC_PADDLE_CLIENT_TOKEN=your_paddle_client_token
```

---

## Available Scripts

### Frontend (`frontend/package.json`)

- `npm run dev` — Start Next.js dev server
- `npm run build` — Build production frontend
- `npm run start` — Start production frontend server
- `npm run lint` — Run ESLint

### Backend (`server/package.json`)

- `npm run dev` — Start API server with Nodemon
- `npm run start` — Start API server with Node.js

---

## API Surface (High-Level)

Backend base path prefixes:

- `/api/auth`
- `/api/documents`
- `/api/ai`
- `/api/flashcards`
- `/api/quizzes`
- `/api/progress`
- `/api/payments`
- `/webhook` (Paddle webhook endpoint)

---

## Deployment Notes

- Set `NODE_ENV=production` in backend.
- Configure strict, correct `CLIENT_URL` values for CORS.
- Ensure all production keys (Paddle, OAuth, AI, Cloudinary, email) are set.
- Configure persistent storage/strategy for uploaded media as needed.
- Verify webhook endpoint accessibility for Paddle events.

---

## Troubleshooting

- **Port conflict on 3000**: run backend on `PORT=8080` and keep frontend on `3000`.
- **CORS errors**: ensure frontend origin is included in backend `CLIENT_URL`.
- **Auth failures**: verify JWT secret and Google client IDs on both client and server.
- **Media generation issues**: ensure FFmpeg is installed and available in PATH.
- **Database connection errors**: verify `MONGODB_URI` and network access.

---

