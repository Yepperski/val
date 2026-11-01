# Vendetta Private Circle

Vendetta is a Vite + React site with a Supabase-backed content editor for the public landing page and manually managed circle members.

## Local setup

1. Install the project dependencies with the repository's existing package manager.
2. Create or update `.env` with:

```env
VITE_SUPABASE_URL=https://YOUR_PROJECT.supabase.co
VITE_SUPABASE_PUBLISHABLE_KEY=YOUR_SUPABASE_ANON_KEY
```

3. Apply `supabase/migrations/20261101000100_manual_vendetta_content.sql` to the Supabase project.
4. Create the first user through Supabase Auth, then insert that user's UUID into `public.user_roles` as an `admin`:

```sql
insert into public.user_roles (user_id, role)
values ('AUTH_USER_UUID', 'admin');
```

5. Start the Vite app and open `/admin`.

## Admin editor

The `/admin` route lets an administrator:

- edit the intro, hero, statement, footer, and music metadata;
- upload a background image, crest image, or audio file to the `site-media` bucket;
- add, edit, hide, reorder, and delete circle members;
- upload member avatars, banners, and optional member-specific music;
- set member bios, music metadata, and social links.

Saved settings and visible members are loaded by the public site. The old Archive, Discord, and bot-connected member surfaces are no longer part of the app navigation or content model.
