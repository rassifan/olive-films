# Olive Films website: setup

The site has two parts:

- **The website** (Home, Films, a page per film, About, Contact), built with Next.js.
- **The admin** at `/admin`, where you add films, upload photos and loops, edit text and read messages. Everything is stored in **Supabase** (database, logins and file storage).

You need three free accounts: **GitHub**, **Supabase** and **Vercel**. You also need your domain, from wherever you bought it.

Until Supabase is connected, the site runs in preview mode with sample content.

---

## 1. Supabase: the database (about 10 minutes)

1. Go to **supabase.com** → New project. Pick the region closest to your audience (for East Africa, Frankfurt or London are usually fastest) and save the database password somewhere safe.
2. Open **SQL Editor → New query**. Paste the whole of `supabase/schema.sql`.
3. On the **last line**, replace `you@example.com` with the email you'll log in with. Then press **Run**.
4. Go to **Authentication → Users → Add user → Create new user**. Use the same email and a strong password, and tick **Auto confirm user**.
5. Go to **Authentication → Sign In / Providers** and turn **off** "Allow new users to sign up". Only the people you add can log in.
6. Go to **Project Settings → API** and copy the **Project URL** and the **anon public** key.

To give someone else admin access, add them as a user (step 4) and run:

```sql
insert into public.admins (email) values ('their@email.com');
```

## 2. Run it on your computer (optional)

You need Node.js 20 or newer.

```bash
cp .env.example .env.local     # then paste your Project URL and anon key into it
npm install
npm run dev                    # open http://localhost:3000 and http://localhost:3000/admin
```

## 3. Put it online with Vercel

1. Upload this folder to a new **GitHub** repository.
2. On **vercel.com** → Add New → Project → import that repository.
3. Under **Environment Variables**, add the values from `.env.example`: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` and `NEXT_PUBLIC_SITE_URL` (your domain, for example `https://olivefilms.com`).
4. Press **Deploy**.

## 4. Connect your domain

1. In Vercel → your project → **Settings → Domains**, add your domain (for example `olivefilms.com`, plus `www.olivefilms.com`).
2. Vercel shows one or two DNS records. Add them where you bought the domain, under DNS settings. It's usually an `A` record pointing to Vercel's address and a `CNAME` for `www`.
3. Wait for the domain to show as valid (minutes to a few hours). HTTPS is set up automatically.

## 5. First steps in the admin

1. Open `yourdomain.com/admin` and sign in.
2. **Site content**: add your showreel loop, a hero still, your email, phone and location.
3. **Films**: *The Land That Chose to Live* is already there as a draft. Add its poster, a short loop and the full-film link, then press **Save and publish**.

## Media guide

| What | Format | Size | Where it shows |
|---|---|---|---|
| Showreel loop | MP4 (H.264), muted, 15–30 s, 1920×1080 | under 50 MB | Homepage hero |
| Film loop | MP4, muted, 5–15 s | under 50 MB | Homepage list, hover on Films |
| Poster | JPG, 16:9, 1920 px wide | under 2 MB | Everywhere a film appears |
| Full film | YouTube, Vimeo or Google Drive link (best), or an MP4 | — | The film's page |
| Photographs | JPG, 2400 px on the long side | under 5 MB each | The film's page, as a photo story |

Supabase's free plan stores 1 GB in total, so put full-length films on YouTube or Vimeo and upload only loops, posters and photos. Vimeo gives the cleanest player. For Google Drive, set the file to "Anyone with the link can view".

To make a small loop, export from your editor at 1080p, H.264, around 4–6 Mbps, no audio. Free tools like HandBrake work too.
