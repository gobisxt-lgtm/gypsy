# ResumeAI - AI-Powered Resume Analysis Platform

## Overview

ResumeAI is a full-stack web application that allows users to upload resumes and receive AI-powered analysis, scoring, and improvement suggestions. The platform uses OpenAI integration for intelligent resume evaluation and provides users with actionable feedback to improve their job prospects.

The application follows a modern React + Express architecture with PostgreSQL for data persistence, featuring Replit Auth for authentication and a polished UI built with shadcn/ui components.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state caching and synchronization
- **Styling**: Tailwind CSS with shadcn/ui component library (New York style)
- **Animations**: Framer Motion for page transitions and micro-interactions
- **Build Tool**: Vite with custom path aliases (@/, @shared/, @assets/)

### Backend Architecture
- **Runtime**: Node.js with Express
- **Language**: TypeScript with ES modules
- **API Design**: RESTful endpoints defined in `shared/routes.ts` with Zod validation
- **Session Management**: Express sessions with PostgreSQL store (connect-pg-simple)

### Data Storage
- **Database**: PostgreSQL with Drizzle ORM
- **Schema Location**: `shared/schema.ts` for shared types between client/server
- **Migrations**: Managed via `drizzle-kit push` command
- **Key Tables**:
  - `users` - User accounts (Replit Auth managed)
  - `sessions` - Session storage for authentication
  - `resumes` - User-uploaded resume content
  - `analyses` - AI-generated resume analysis results
  - `conversations` / `messages` - Chat functionality support

### Authentication
- **Provider**: Replit Auth (OpenID Connect)
- **Implementation**: Passport.js with custom OIDC strategy
- **Session Storage**: PostgreSQL-backed sessions with 1-week TTL
- **Protected Routes**: Server middleware checks `req.isAuthenticated()`

### AI Integration
- **Provider**: OpenAI API via Replit AI Integrations
- **Client Location**: `server/openai.ts`
- **Features Used**:
  - Text completions for resume analysis
  - Image generation capabilities (gpt-image-1)
  - Voice/audio processing with speech-to-text
- **Rate Limiting**: Built-in batch processing utilities with retry logic

### Build System
- **Development**: `tsx` for TypeScript execution with Vite dev server
- **Production Build**: 
  - Frontend: Vite builds to `dist/public`
  - Backend: esbuild bundles to `dist/index.cjs`
  - Dependencies allowlist for optimized cold starts

## External Dependencies

### Database
- PostgreSQL (required, connection via DATABASE_URL environment variable)
- Drizzle ORM for type-safe queries
- connect-pg-simple for session storage

### Authentication
- Replit Auth (OpenID Connect provider)
- Required env vars: ISSUER_URL, REPL_ID, SESSION_SECRET

### AI Services
- OpenAI API via Replit AI Integrations
- Required env vars: AI_INTEGRATIONS_OPENAI_API_KEY, AI_INTEGRATIONS_OPENAI_BASE_URL

### UI Components
- shadcn/ui (Radix UI primitives)
- Tailwind CSS
- Lucide React icons
- date-fns for date formatting
- recharts for data visualization

### Development Tools
- Vite with HMR
- Replit-specific plugins (cartographer, dev-banner, runtime-error-modal)