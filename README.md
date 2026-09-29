# CodeMind — Hindsight-powered AI Code Review

CodeMind is a protected code-review workspace designed around persistent engineering memory.

## What changed in this version

- Secure server-side authentication with hashed passwords and signed sessions.
- Review API requires authentication.
- New UI/UX: dark developer workspace, memory flow, responsive layout.
- Removed the hard-coded demo review fallback.
- New-code reviews are generated from the actual submitted source.
- Dynamic local checks work without an LLM.
- Optional Groq LLM review can deepen analysis.
- Hindsight recall is based on signals extracted from the current code.
- Useful findings are retained for future reviews.
- Hindsight and LLM credentials remain server-side.
- Request-size validation and lightweight rate limiting added.

## Run

```bash
npm install
copy .env.example .env
npm run dev
```

Open the Vite URL shown in the terminal.

In another terminal:

```bash
npm run server
```

Create an account in the app. Then submit the starter code or replace it with completely new code.

## Optional Hindsight

Set these in `.env`:

```env
HINDSIGHT_API_URL=https://api.hindsight.vectorize.io
HINDSIGHT_API_KEY=your_key
HINDSIGHT_BANK_ID=codemind-team
```

Hindsight's current TypeScript SDK supports `retain` and `recall`; CodeMind keeps these calls on the server. See the official docs:
https://docs.hindsight.vectorize.io/typescript-sdk/

## Optional LLM

```env
GROQ_API_KEY=your_key
GROQ_MODEL=openai/gpt-oss-120b
```

If the LLM is not configured or temporarily fails, CodeMind still performs dynamic local analysis rather than returning a fixed example.

## Important

This authentication is suitable for the hackathon prototype. For production deployment, use a managed identity provider/database, HTTPS, secure cookies, CSRF protection, account recovery, email verification, and persistent server-side session storage.

Never commit `.env` or `server/data/users.json`.


### Guest access
The sign-in screen includes **Continue as Guest** for temporary demo/testing access. Guest sessions are signed server-side, expire after 2 hours, and do not require a password. Use a registered account for normal authenticated development work.
