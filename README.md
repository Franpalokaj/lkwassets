# lkw-email-assets

Static image host for LKW.APP email campaigns, deployed on Vercel and served from
the branded subdomain **`assets.lkw.app`**. Plain static files — no build step.

## Structure

```
nav-beta/                  → served at https://assets.lkw.app/nav-beta/<file>
  00-hero.jpg              Email header banner
  00b-testflight.png       iOS install (TestFlight) screenshot
  01-login.png             Step 1 — log in
  02-truck-profile.png     Step 2 — truck profile
  03-destination.png       Step 3 — destination
  04-start.png             Step 4 — start
  05-navigation.png        Step 5 — drive
  06-feedback.png          Step 6 — in-app feedback form
```

`vercel.json` sets `Access-Control-Allow-Origin: *` and 1-year immutable caching on
`/nav-beta/*`.

## Deploy

```bash
npm i -g vercel          # if not installed
vercel login
vercel --prod            # from this directory; first run links/creates the project
```

## Custom domain (one-time)

1. In the Vercel project → **Settings → Domains → Add** `assets.lkw.app`.
2. Vercel shows a DNS target. In **IONOS DNS** for `lkw.app`, add a **CNAME**:
   - Host/Name: `assets`
   - Points to: `cname.vercel-dns.com` (use whatever Vercel specifies)
3. Wait for verification. Images are then live at
   `https://assets.lkw.app/nav-beta/01-login.png`.

## Using in emails

The email templates reference images by the local prefix
`nav-beta-web/email-assets/nav-beta/`. Before sending, find-replace that prefix with
`https://assets.lkw.app/nav-beta/`.

## Versioning rule

Emails live in inboxes forever — never overwrite a file in place after a send.
If a screenshot is re-cropped, add a new versioned filename (e.g. `01-login-v2.png`)
and update the email reference. Old sends keep working.
