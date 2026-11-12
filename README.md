# Company Knowledge Base Chatbot

A starter RAG application: Next.js frontend + Python Vercel functions + OpenAI + Supabase pgvector.

## Setup
1. Create a Supabase project.
2. Run `supabase/schema.sql` in Supabase SQL Editor.
3. Create a **private** Supabase Storage bucket named `company-documents`.
4. Copy `.env.example` to `.env.local` and fill in the keys.
5. Run `npm install`, then `npm run dev` for the frontend.
6. For local Python serverless endpoints, install Vercel CLI and run `vercel dev`.

## Deploy
Push to GitHub, import the repository into Vercel, set the environment variables from `.env.example`, and deploy from the repository root.

## Environment variables
- `OPENAI_API_KEY`: server-only OpenAI key.
- `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`: server-only Supabase credentials.
- `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`: browser-safe Supabase settings (RLS must remain enabled).

## Endpoints
- `GET /api/health`
- `POST /api/upload` (multipart: file, department, category)
- `POST /api/chat` (JSON: `{"question":"..."}`)
- `GET /api/documents`
- `DELETE /api/documents?id=<uuid>`

All except health require `Authorization: Bearer <Supabase access token>`.

## Important
This is a portfolio MVP, not a fully audited enterprise deployment. It supports PDF, DOCX, and TXT; uploads are limited to 4 MB. Vercel functions are stateless and have execution limits. For large documents or high traffic, move ingestion to a background worker. Add organization/team membership and role-based access before using it across a real company. Never expose the OpenAI key or Supabase service-role key in frontend code.
