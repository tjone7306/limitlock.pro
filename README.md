# LimitLock — limitlock.pro landing site

Static landing page for LimitLock, set up for GitHub Pages with a custom domain.

## Files

- `index.html` — main landing page (rugged outdoor theme, dark greens + gold accent)
- `privacy-policy.html` — privacy policy
- `support.html` — support / FAQ
- `404.html` — custom not-found page
- `CNAME` — tells GitHub Pages to serve on `limitlock.pro`
- `screenshots/` — four SVG phone mockups used in the hero + gallery

## One-time setup

### 1. Create the GitHub repo

On github.com, signed in as **tjone7306**:

1. Click the **+** (top right) → **New repository**
2. Repository name: `limitlock.pro` (recommended — matches the domain)
3. Visibility: **Public** (required for free GitHub Pages)
4. Leave everything else empty (no README, no .gitignore)
5. Click **Create repository**

### 2. Push this folder

Open Terminal on your Mac and run:

```bash
cd ~/Documents/Claude/Projects/Fish\ Culling/limitlock-site
git init -b main
git add .
git commit -m "Initial landing site"
git remote add origin https://github.com/tjone7306/limitlock.pro.git
git push -u origin main
```

If it prompts for a password, GitHub wants a **personal access token** (not your account password). Create one at github.com → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token with the `repo` scope.

### 3. Enable GitHub Pages

On the repo page:

1. **Settings** → **Pages** (left sidebar)
2. Under **Build and deployment** → **Source**, choose **Deploy from a branch**
3. **Branch**: `main`, **Folder**: `/ (root)` → **Save**
4. Wait ~1 minute. GitHub will show "Your site is live at https://tjone7306.github.io/limitlock.pro/"

### 4. Point limitlock.pro at GitHub Pages (GoDaddy DNS)

GitHub Pages apex-domain IPs (as of this writing):

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

On **godaddy.com** → **My Products** → **Domains** → **limitlock.pro** → **DNS**:

**Delete** any existing `A` records for `@` and any `CNAME` record for `www` that GoDaddy added by default (parked-page / forwarding records).

**Add these records:**

| Type  | Name | Value                        | TTL    |
|-------|------|------------------------------|--------|
| A     | @    | `185.199.108.153`            | 1 hour |
| A     | @    | `185.199.109.153`            | 1 hour |
| A     | @    | `185.199.110.153`            | 1 hour |
| A     | @    | `185.199.111.153`            | 1 hour |
| CNAME | www  | `tjone7306.github.io`        | 1 hour |

Save. DNS usually propagates in 5–30 minutes (occasionally longer).

### 5. Turn on HTTPS

Back in the GitHub repo:

1. **Settings** → **Pages**
2. Under **Custom domain**, confirm it shows `limitlock.pro` (the `CNAME` file already sets this — it should auto-detect)
3. Wait for the green check on "DNS check successful"
4. Tick **Enforce HTTPS**

That's it. `https://limitlock.pro` will serve this page, and `https://www.limitlock.pro` will redirect to it.

## Updating the site later

Make changes on your Mac, then:

```bash
cd ~/Documents/Claude/Projects/Fish\ Culling/limitlock-site
git add .
git commit -m "Update site"
git push
```

GitHub Pages rebuilds in ~30 seconds.
