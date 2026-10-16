# Karnataka News 24

Kannada-first, English-optional responsive news portal using Next.js 15, Supabase Auth/Postgres and row-level security.

## Features
- Kannada homepage and 10 news categories
- Full news articles with optional English text in expandable section
- Email/password admin login
- Protected admin publishing dashboard (create, edit, delete, draft/publish)
- Public users can only read published news; only approved editors can manage articles
- Mobile-responsive design

## Local setup
1. Install Node.js 20.9+ and create a free Supabase project at https://supabase.com.
2. Open Supabase **SQL Editor**, paste and run `supabase/schema.sql`.
3. Under **Authentication > Users**, create your editor user (email/password) using the dashboard. Do not enable public sign-up unless you need it.
4. Copy the user's UUID from Authentication > Users. In SQL Editor run:
   `insert into public.admins(user_id) values ('PASTE-USER-UUID-HERE');`
   This step requires dashboard owner privileges. Never place a Supabase service-role key in the browser.
5. Copy `.env.example` to `.env.local`. Set `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY` from Supabase project settings/API keys (use the publishable or legacy anon key, never the secret key).
6. In a terminal run `npm install` then `npm run dev`.
7. Visit http://localhost:3000 and http://localhost:3000/login. Publish your first story in `/admin`.

## Free deployment (recommended: Vercel)
1. Push this folder to a private or public GitHub repository.
2. Import the repository at https://vercel.com/new, choose the Next.js framework preset.
3. Set the two environment variables from `.env.local` in Vercel project settings. Deploy.
4. In Supabase Authentication > URL Configuration, set Site URL to your deployed HTTPS address and add it to redirect URLs if you later use OAuth/email links.
5. Use the free `.vercel.app` address. Free-tier quotas and platform eligibility apply; review Vercel's current hobby plan terms before using the site commercially. For commercial news publishing, choose a host/plan that permits it.

## Editorial notes
- Verify sources and obtain permission for news photos; do not copy copyrighted articles.
- Never publish personal data or allegations without verification.
- Add a Privacy Policy, Contact, Corrections and About page before public launch.
- This starter accepts an externally hosted image URL; it does not upload images.
- There is no automated translation: provide English article fields manually when desired.
- Do not rely on this starter as a fully production-hardened CMS; add rate limiting, backups, monitoring, moderation and accessibility checks for a public newsroom.

## Optional production improvement
Upgrade to a current supported Next.js release and test compatibility before launch. This starter uses the Next.js 15 `middleware.ts` convention for refreshing Supabase sessions.
