# DocuMind AI — Next-Gen Document Intelligence & Analysis Platform

> **AI Project (CSE276)**  
> **Repository:** [abdulbaque005-creator/AI_PROJECT_CSE276](https://github.com/abdulbaque005-creator/AI_PROJECT_CSE276)

[![Next.js](https://img.shields.io/badge/Next.js-16.4.3-black?logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19.3.0-blue?logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue?logo=typescript)](https://www.typescriptlang.org/)
[![Google Gemini](https://img.shields.io/badge/AI-Google%20Gemini%201.5%20%2F%202.0-8E75C4?logo=google)](https://ai.google.dev/)
[![Prisma](https://img.shields.io/badge/ORM-Prisma%206-2D3748?logo=prisma)](https://www.prisma.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-v4-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)

---

## 📌 Project Overview

**DocuMind AI** is an intelligent, multi-tenant document analysis, multi-document synthesis, and automated artifact generation platform. Engineered for deep comprehension of diverse data formats, DocuMind turns unstructured files into actionable intelligence with verified citations and interactive analytics.

Powered by Google's frontier Gemini models (`gemini-1.5-flash`, `gemini-1.5-pro` with up to 2M context window, and `gemini-2.0-flash`), DocuMind allows users to upload complex documents, converse in natural language, uncover hidden patterns in spreadsheets, and generate polished deliverables (DOCX, PDF, Markdown, Spreadsheets, and Charts).

---

## ✨ Key Features & Capabilities

### 1. Multi-Format Ingestion & Analysis
- **PDF Documents (`pdf-parse`)**: Page-by-page layout extraction, metadata harvesting, and chunking.
- **Office Files (`mammoth`, `exceljs`)**: Full text and structural extraction for Microsoft Word (`.docx`) and Excel (`.xlsx`).
- **Data & Tables (`papaparse`)**: CSV and JSON tabular parsing for structured queries and statistical breakdowns.
- **Visual & Multimodal (`sharp`)**: Image processing and OCR-readiness for PNG, JPEG, and WebP.
- **Plain Text & Markdown**: Semantic chunking preserving heading and table boundaries.

### 2. Multi-Model AI Reasoning Engine
- **Google Gemini 1.5 Flash**: Low-latency, high-throughput question-answering with a 1M token context window.
- **Google Gemini 1.5 Pro**: Deep reasoning, cross-document comparison, and multi-file synthesis across up to 2M tokens.
- **Google Gemini 2.0 Flash**: Next-generation multimodal model for real-time document interaction.
- **Strict Anti-Hallucination Guardrails**: Explicit retrieval ground rules that notify users when no evidence exists rather than fabricating answers.

### 3. Precision Citations & Provenance
- Every answer points back to the exact source document, page number, and chunk index (`[DocumentName, p.X]`).
- Side-by-side evidence previewing for full auditability.

### 4. Interactive Spreadsheet & Data Intelligence
- Automated dataset profiling: column data types, row counts, and structural anomalies.
- Pattern, trend, and outlier detection with step-by-step reasoning.
- Natural-language querying for financial, academic, and business spreadsheets.

### 5. Dynamic Generative Artifact Studio
- Automatically produces structured deliverables from conversations:
  - **Documents & Reports**: Structured research reports and executive summaries.
  - **Spreadsheets**: Generated tables and datasets ready for export.
  - **Visualizations & Charts**: Markdown and code artifacts for data presentation.

### 6. Resilient Storage & Asynchronous Processing
- **Pluggable Storage**:
  - Local disk storage (zero-configuration local development).
  - Cloudflare R2 (S3-compatible, zero egress fees).
  - AWS S3 or MinIO.
- **BullMQ Queue with Synchronous Fallback**: Document ingestion is managed via Redis and BullMQ background workers, gracefully degrading to synchronous execution when Redis is unavailable.
- **Multi-Tenant Workspaces**: Role-based access control (Owner, Member, Viewer), folder trees, and session management via NextAuth.js.

---

## 🛠️ Technology Stack

| Layer | Technology |
|---|---|
| **Framework** | Next.js 16 (App Router), React 19, TypeScript |
| **Styling & UI** | Tailwind CSS v4, Lucide Icons, Motion (Framer), Shadcn UI, Base UI |
| **AI SDK & Models** | Vercel AI SDK (`ai`, `@ai-sdk/google`), Google Gemini 1.5 / 2.0 |
| **Database & ORM** | PostgreSQL (Neon / Supabase / Local), Prisma ORM 6.4 |
| **Authentication** | NextAuth.js (v5 beta) with Credentials and Google OAuth |
| **File Extractors** | `pdf-parse`, `mammoth`, `exceljs`, `papaparse`, `sharp` |
| **Background Queue**| BullMQ, Redis (with sync processing fallback) |
| **Storage Modes** | Local File System, AWS S3, Cloudflare R2 |

---

## 📂 Project Architecture

```
documind-ai/
├── prisma/
│   ├── migrations/       # Database migration history
│   ├── schema.prisma     # Prisma data schema (Workspaces, Documents, Chunks, Messages, Artifacts)
│   └── seed.ts           # Initial database seeding script
├── public/               # Static assets & icons
├── scripts/              # Migration, verification, and E2E lifecycle test scripts
├── src/
│   ├── app/
│   │   ├── (auth)/       # Authentication routes (login, register)
│   │   ├── (workspace)/  # Main workspace, document view, and chat routes
│   │   ├── api/          # REST & streaming endpoints (documents, chat, upload)
│   │   ├── globals.css   # Theme and Tailwind styling
│   │   ├── layout.tsx    # Root layout and providers
│   │   └── page.tsx      # Landing page
│   ├── components/
│   │   ├── artifacts/    # Interactive artifact viewer and editor
│   │   ├── chat/         # Conversational interface with citation badges
│   │   ├── documents/    # Upload modal, document grid, and folder tree
│   │   ├── layout/       # Workspace sidebar, navbar, and headers
│   │   └── ui/           # Reusable UI component library
│   ├── hooks/            # Custom React hooks (model selection, keyboard shortcuts)
│   ├── lib/
│   │   ├── ai/           # Gemini provider registration, system prompts, streaming
│   │   ├── db/           # Prisma client singleton
│   │   ├── documents/    # Extractors (PDF, DOCX, XLSX, CSV, images), chunker, retrieval
│   │   ├── queue/        # BullMQ document processing queues
│   │   └── storage/      # Local, S3, and Cloudflare R2 storage drivers
│   ├── stores/           # Zustand state management (workspace, UI)
│   └── types/            # TypeScript schemas for documents, chat, artifacts, AI
└── workers/
    └── process.ts        # Standalone worker for background document ingestion
```

---

## 🚀 Getting Started

### 1. Prerequisites
- **Node.js**: v20 or higher
- **npm**, **pnpm**, or **yarn**
- **PostgreSQL**: Local instance or cloud database (Neon, Supabase)
- **Google AI Studio API Key**: For Gemini models ([Get API Key](https://aistudio.google.com/))
- **Redis** *(Optional)*: For background BullMQ queue processing

### 2. Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/abdulbaque005-creator/AI_PROJECT_CSE276.git
cd AI_PROJECT_CSE276
npm install
```

### 3. Environment Setup

Copy `.env.example` to `.env`:

```bash
cp .env.example .env
```

Configure your environment variables:

```env
# Database
DATABASE_URL="postgresql://user:password@localhost:5432/documind?schema=public"
DIRECT_URL="postgresql://user:password@localhost:5432/documind?schema=public"

# Auth
AUTH_SECRET="generate-a-random-secret-at-least-32-chars"
AUTH_URL="http://localhost:3000"

# AI Provider
GOOGLE_GENERATIVE_AI_API_KEY="your-gemini-api-key"

# Storage (Defaults to local disk storage, zero cloud credentials required)
STORAGE_MODE="local"
LOCAL_STORAGE_DIR=".storage/documents"

# Redis (Optional — defaults to synchronous processing if not reachable)
REDIS_URL="redis://localhost:6379"
```

### 4. Database Setup

Generate Prisma Client and apply migrations:

```bash
npx prisma generate
npx prisma migrate dev --name init
```

*(Optional) Seed the database with sample workspace data:*

```bash
npm run seed # or npx tsx prisma/seed.ts
```

### 5. Running the Application

Start the Next.js development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

*(Optional)* If running asynchronous background workers with BullMQ:

```bash
npx tsx workers/process.ts
```

---

## 📄 License & Attribution

Developed as an Artificial Intelligence Project (**CSE276**).  
Author: [abdulbaque005-creator](https://github.com/abdulbaque005-creator)
