# EduAI Nexus

AI-Powered Smart Education Ecosystem for India — a hackathon POC with 6 interactive AI modules for students, teachers, and policymakers.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 8080)
- `pnpm --filter @workspace/eduai-nexus run dev` — run the frontend (port 23786)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- Frontend: React + Vite, Tailwind CSS, Framer Motion, Recharts, Lucide React
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- AI: Anthropic Claude (via Replit AI Integrations — no user key needed)
- Validation: Zod (zod/v4), drizzle-zod
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/eduai-nexus/` — React frontend with 7 pages
- `artifacts/api-server/` — Express API server
- `lib/api-spec/openapi.yaml` — Single source of truth for API contracts
- `lib/db/src/schema/` — Drizzle ORM schemas (conversations, messages)
- `lib/integrations-anthropic-ai/` — Replit-managed Anthropic client

## Architecture decisions

- All Claude API calls go through the backend (api-server), never directly from frontend — keeps keys secure
- SSE streaming for Career Coach chat — real-time token streaming via ReadableStream on the client
- OpenAPI-first contract: spec in `lib/api-spec/openapi.yaml` → codegen → typed hooks + Zod schemas
- Deep navy + electric teal design system, dark-mode-only (no light mode toggle needed for hackathon)
- Replit AI Integrations for Anthropic — no API key required, billed to Replit credits

## Product

**6 AI-Powered Modules:**
1. `/learn` — Personalised Learning Engine: PDF-to-MCQ generator, performance charts, flashcards, learning styles
2. `/labs` — Virtual Labs: Interactive physics pendulum simulation with AI explanation
3. `/translate` — Multilingual Learning: Translate & simplify concepts in 8 Indian languages
4. `/career` — Career Readiness: ATS analyzer, skill gap analysis, streaming career coach chat
5. `/dashboard` — Smart Resource Allocation: Policymaker dashboard with district-wise charts and forecasts
6. `/projects` — Micro-Project Learning: AI-generated project ideas and opportunities feed

## User preferences

- Team badge: "Team MAHADEV | WitchHunt 2026" in the footer

## Gotchas

- After changing openapi.yaml, always run codegen before using types
- The Anthropic client uses Replit AI Integration env vars (auto-provisioned, do not modify)
- Claude model to use: claude-sonnet-4-6 (NOT claude-sonnet-4-20250514 — that model is not available via Replit AI Integrations)
- SSE streaming endpoint cannot use generated React Query hooks — must use fetch + ReadableStream

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
