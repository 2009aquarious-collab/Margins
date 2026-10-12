# Moss & Margin — public website + accounts

This is a static HTML version of Moss & Margin with the existing sage-green design, local autosave/backup, delete/restore tools, and a Supabase integration for email/password + Google login and private per-account cloud saving.

## 1) Create the cloud project (one-time)
1. Create a project at https://supabase.com/ and save the database password somewhere safe.
2. In the project, open **SQL Editor**, create a query, paste all of `supabase-setup.sql`, and run it.
3. Open **Project Settings → API** (or API Keys). Copy the Project URL and the publishable key (older projects may call it the `anon` key).
4. Put those values into `config.js`. Never use a `service_role` or secret key in this HTML project.
5. Open **Authentication → URL Configuration**. Add your deployed website URL to Site URL and Redirect URLs (you can add localhost while testing).
6. In **Authentication → Providers**, enable Email. For Google login, enable Google and follow Supabase's Google provider instructions: https://supabase.com/docs/guides/auth/social-login/auth-google. This requires a Google Cloud OAuth client and a redirect URI supplied by Supabase.

## 2) Publish it (simple static hosting)
1. Create a GitHub repository and upload `index.html`, `config.js`, and `supabase-setup.sql` (you may also keep this README).
2. Rename `moss_and_margin_cloud.html` to `index.html` before uploading.
3. In Netlify, choose **Add new site → Import an existing project**, connect GitHub, select the repository, and deploy. No build command is needed; publish directory is `/` (repository root).
4. Add the resulting `https://...netlify.app` URL to Supabase Authentication → URL Configuration. Redeploy if needed.

Alternative: drag-and-drop the folder to Netlify Drop for a quick public preview. Git-based deploy is better for future updates.

## 3) Test safely
- Open the public URL in a private/incognito window.
- Create an account with email/password; confirm the email if confirmation is enabled.
- Sign in, create a test chapter, wait for “Synced ✓”, then open the site on another browser/device and sign into the same account.
- Test Google only after configuring the provider.
- Export a local backup from Settings → Writing safety before testing restore or deletion.

## Important notes
- The website is public, but each user's workspace is private via Row Level Security. Do not remove the SQL policies or expose a service-role key.
- Email/password and cloud sync only work after you create/configure your own Supabase project. Google login also requires Google OAuth configuration.
- Local autosave and backup/export remain available if cloud setup is incomplete or the user is signed out.
- This prototype stores the whole workspace snapshot in one JSON row per account. For a larger production app, split books/chapters/characters into individual tables and add testing, account recovery, privacy terms, and a proper delete-account flow.
