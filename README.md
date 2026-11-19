# teamtouchtype.com

The Team TouchType studio site. Static HTML and CSS; there's no build step.

| Path | File | What |
|---|---|---|
| `/` | `index.html`, `home.css` | Studio home with the Games section |
| `/legion/` | `legion/index.html`, `legion/style.css` | Legion: Rise of the Order splash page |
| | `assets/` | Shared images (Legion art, favicon, link-preview image) |

- **Preview locally:** `python -m http.server 8000`, then open http://localhost:8000
- **Add a game:** copy the `<a class="game game--legion">` block in `index.html`, and give the new game its own folder like `legion/`.
- **Add a Legion store link:** in `legion/index.html`, replace the "Coming soon" line with the commented-out `cta` link.
- **Change the Legion cards:** swap the files in `assets/` (card art comes from `legion/assets/art/cards/` in the game repo).

## Deploy with Cloudflare Pages (recommended, since the domain is on Cloudflare)

1. Push this repo to GitHub.
2. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git** → pick `TeamTouchType/landing-page`.
3. Build settings: Framework preset **None**, build command **empty**, output directory **`/`**. Click **Save and Deploy**.
   You get a `*.pages.dev` URL in about a minute.
4. In the project, open **Custom domains** → **Set up a custom domain** → enter `teamtouchtype.com` (and again for `www.teamtouchtype.com`).
   Since the domain's DNS is already on Cloudflare, it adds the records and HTTPS for you.

Every push to `main` redeploys automatically.

## Or: Netlify

1. Netlify → **Add new site** → **Import an existing project** → GitHub → `TeamTouchType/landing-page`.
2. Build command **empty**, publish directory **`.`** → **Deploy**.
3. **Domain management** → **Add a domain** → `teamtouchtype.com`.
4. In Cloudflare **DNS**, add:
   - `CNAME` `@` → `<your-site>.netlify.app`
   - `CNAME` `www` → `<your-site>.netlify.app`

   Set both to **DNS only** (grey cloud), so Netlify can issue the HTTPS certificate.
5. Back in Netlify, wait for the certificate under **HTTPS** (a few minutes).

(No Git? Both hosts also let you drag-and-drop this folder: Cloudflare Pages → **Upload assets**, Netlify → **Deploy manually**.)
