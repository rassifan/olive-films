# Olive Films

The Olive Films website: a documentary studio site with its own admin.

- **Website:** Home (showreel hero, selected films, statement, client marquee, contact), Films (filterable grid), a case-study page per film (player, impact slate, story, photo story), About, Contact.
- **Admin** (`/admin`): add and order films, upload posters, loops and photos or paste YouTube / Vimeo / Drive links, edit homepage and About text, read contact-form messages.
- **Built with** Next.js 14, Supabase (database, login, storage) and the Olive Films brand: Big Shoulders Display, Archivo, IBM Plex Mono, Night palette, the reel mark.

Setup and hosting steps are in [SETUP.md](./SETUP.md).

```
app/(site)/          public pages
app/admin/           admin (login, films, site content, messages)
components/          shared pieces (Frame, Player, film grid, contact form)
lib/                 data loading, Supabase clients, link parsing
supabase/schema.sql  database, security rules and storage
public/brand/        logo files
```
