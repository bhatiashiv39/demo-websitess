# Rohtak Public School — website management demo

A plain HTML/CSS/JS demo site (no build step) for a school in Rohtak, with a
Supabase backend for notices, admission enquiries, and contact messages, and
a staff login page to publish notices. Rename "Rohtak Public School" and the
placeholder details throughout the HTML to match your actual school.

## Files

```
index.html          Home page (pulls latest notices from Supabase)
notices.html         Full notices list
admissions.html       Admission info + enquiry form
gallery.html          Photo gallery (static placeholders — swap in images/)
contact.html          Contact info + message form
admin.html             Staff login + notice management dashboard
css/style.css          All styling
js/supabase-client.js   Supabase project URL + anon key (edit this)
js/main.js              Shared nav + date helper
js/admin.js             Admin dashboard logic (auth, notice CRUD)
supabase/schema.sql     Database tables + Row Level Security policies
```

## 1. Set up Supabase

1. Create a project at supabase.com.
2. Open **SQL Editor** and run the contents of `supabase/schema.sql`. This
   creates the `notices`, `admission_enquiries`, and `contact_messages`
   tables with Row Level Security so the public can read notices and submit
   forms, but only logged-in staff can post notices or read enquiries.
3. Go to **Authentication -> Users** and add a staff account (email +
   password) — this is what you'll use to log in at `admin.html`.
4. Go to **Project Settings -> API** and copy your **Project URL** and
   **anon public key**.

## 2. Connect the site to Supabase

Open `js/supabase-client.js` and replace the two placeholder values:

```js
const SUPABASE_URL = "https://YOUR-PROJECT-REF.supabase.co";
const SUPABASE_ANON_KEY = "YOUR-ANON-PUBLIC-KEY";
```

The anon key is safe to expose in frontend code — the RLS policies in
`schema.sql` control what it's allowed to do.

## 3. Push to GitHub

```bash
cd school-site
git init
git add .
git commit -m "Initial school website"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main
```

## 4. Host on Cloudflare Pages

1. Cloudflare dashboard -> **Workers & Pages -> Create -> Pages -> Connect to Git**.
2. Pick your repository.
3. Build settings: leave **Build command** and **Build output directory**
   blank (or set output directory to `/`) — this is a static site, no build
   step needed.
4. Deploy. Cloudflare gives you a `*.pages.dev` URL; add a custom domain
   under the project's **Custom domains** tab if you have one.

## Using the admin dashboard

Go to `/admin.html`, log in with the staff account you created in Supabase
Auth, and use the form to publish notices — they appear immediately on the
home page's noticeboard and on `/notices.html`. The dashboard also lists
recent admission enquiries submitted through the site.

## Customizing

- Replace the placeholder school name, address, phone, stats, and table
  values in each HTML file.
- Swap the gallery placeholders in `gallery.html` for real `<img>` tags
  pointing at photos you add to `images/`.
- Colors and fonts are defined as CSS variables at the top of
  `css/style.css`.
