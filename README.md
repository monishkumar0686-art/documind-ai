# DocuMind AI

**Understand your documents. Ask better questions. Learn faster.**

A full-stack PDF intelligence workspace: upload text-based PDFs, chat with their contents, generate summaries, extract key insights and create quizzes.

## Stack
React + Vite + Tailwind + Lucide · Node + Express · pdf-parse · Google Gemini API · local JSON persistence with optional Firestore metadata.

## Run locally
Requirements: Node.js 20+, npm, and a Gemini API key from https://aistudio.google.com/app/apikey.

```bash
git clone https://github.com/monishkumar0686-art/documind-ai.git
cd documind-ai
npm install
cp server/.env.example server/.env
```

Add `GEMINI_API_KEY=your_key_here` to `server/.env`, then run:

```bash
npm run dev
```

Open http://localhost:5173. API health: http://localhost:4000/api/health. Build with `npm run build`; API production start: `npm start`.

## Features
- PDF upload, validation, text extraction and page-labelled chunks
- Document-grounded Q&A with page citations and abstention behavior
- AI summary, key takeaways and multiple-choice quiz
- Document search, delete and responsive workspace
- Gemini key server-side, Helmet headers and rate limiting
- Local JSON storage by default; optional Firebase Firestore metadata

## Environment
`GEMINI_API_KEY` (required for AI), `GEMINI_MODEL` (default `gemini-2.5-flash`), `PORT` (4000), `MAX_FILE_SIZE_MB` (20), `CLIENT_ORIGIN`, optional `FIREBASE_SERVICE_ACCOUNT_JSON` and `FIREBASE_PROJECT_ID`.

Without Firebase credentials, metadata is stored in `server/data/documents.json` and PDFs in `server/uploads/`.

## API
- GET /api/health
- GET /api/documents
- POST /api/documents (multipart field: `file`)
- DELETE /api/documents/:id
- POST /api/documents/:id/chat
- POST /api/documents/:id/summary
- POST /api/documents/:id/key-points
- POST /api/documents/:id/quiz

## Security and limitations
The demo uses an `x-owner-id` header with a default local identity. This is a development partition, **not authentication**. Before public deployment, implement Firebase Auth (or another identity provider), verify tokens server-side and derive ownership from verified identity. Use HTTPS, configure CORS and private object storage. Local disk is not suitable for ephemeral hosting. Scanned PDFs need OCR (not included); retrieval currently uses lexical ranking rather than embeddings/vector search.

## Verify before demo
- [ ] Upload a valid PDF; test non-PDF, corrupt, oversized and scanned files.
- [ ] Test answerable and unanswerable questions and page citations.
- [ ] Generate summary, key points and quiz.
- [ ] Test missing Gemini key, deletion and persistence after restart.

This checklist is for verification, not a claim that every scenario has been tested.

## Roadmap
Authentication, OCR, vector search, saved conversation history, multi-document search and exports.
