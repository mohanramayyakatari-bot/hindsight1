# CodeMind database setup

## Recommended: Supabase

CodeMind is prepared for **Supabase Auth + PostgreSQL**. Supabase gives you authentication, a hosted Postgres database, and Row Level Security in one place.

### 1. Create a Supabase project
Create a project and open the SQL Editor.

### 2. Run the schema
Copy `supabase/schema.sql` into the SQL Editor and run it.

### 3. Configure email authentication
For a simple hackathon demo, configure Email/Password authentication according to your desired confirmation flow. If email confirmation is enabled, a newly registered user must confirm their email before a session is returned.

### 4. Configure `.env`
Copy `.env.example` to `.env` and set:

- `SUPABASE_URL`
- `SUPABASE_PUBLISHABLE_KEY`
- `SUPABASE_SECRET_KEY`
- `ADMIN_EMAIL`
- `HINDSIGHT_API_KEY`
- `HINDSIGHT_BANK_ID`
- `GROQ_API_KEY`

The **publishable** key may be used by public application code when RLS is correctly configured. The **secret** key bypasses RLS and must stay on the backend only.

### 5. What gets stored
- `auth.users`: Supabase-managed authentication identity.
- `profiles`: name, email, avatar and login timestamps.
- `review_history`: each authenticated user's review metadata, findings and memory usage. Source code itself is not stored unless `STORE_REVIEW_SOURCE=true`.

Guest sessions remain temporary and do not create a permanent account.

## Other database options

| Option | Best for | CodeMind fit |
|---|---|---|
| **Supabase/Postgres** | Auth + hosted DB + RLS | **Recommended** |
| Firebase/Firestore | Fast NoSQL/mobile apps | Good, but less natural for relational review history |
| MongoDB Atlas | Flexible document data | Good, but extra auth architecture |
| Neon/Postgres | Hosted Postgres | Good, but auth is separate |
| PlanetScale/MySQL | Hosted relational DB | Good, but auth is separate |
| SQLite | Local prototype | Good fallback, not ideal for multi-user deployment |

For this project, Supabase keeps authentication, user profiles, review history and authorization in one ecosystem.
