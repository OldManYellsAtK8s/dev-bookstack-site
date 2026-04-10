# dev-bookstack-site

Static documentation site for [dev-bookstack](https://github.com/OldManYellsAtK8s/dev-bookstack).

## CI / CD

`.github/workflows/deploy.yml` runs on every push and pull request to `main`:

| Job        | What it does                                                                                       |
| ---------- | -------------------------------------------------------------------------------------------------- |
| **Test**   | Lints all HTML with `htmlhint`; checks every local `href`/`src` reference resolves to a real file  |
| **Deploy** | Publishes the site to GitHub Pages — only on a push to `main`, and only if tests pass              |

## Hosting

The site is plain HTML/CSS — no build step, no dependencies. Any static file host works.

### GitHub Pages (automated)

The included workflow deploys the site automatically. You only need to enable Pages once:

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Set **Source** to **GitHub Actions** (not "Deploy from a branch").
4. Push to `main` — the workflow tests and deploys the site. The URL is printed in the workflow run summary.

To use a custom domain, add a `CNAME` file to the repo root containing your domain (e.g. `docs.example.com`) and configure the DNS record per [GitHub's instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site).

### Netlify

Drop the repository folder onto [netlify.com/drop](https://app.netlify.com/drop) for an instant deploy, or connect the GitHub repo for continuous deployment on every push to `main`.

No build command or publish directory configuration is needed — Netlify serves `index.html` from the root automatically.

### Cloudflare Pages

1. Connect the GitHub repo in the Cloudflare Pages dashboard.
2. Leave **Build command** blank and set **Build output directory** to `/`.
3. Deploy. Cloudflare will serve the site globally via its CDN.

### Local preview

```bash
# Python (built-in)
python3 -m http.server 8080

# Node (npx, no install required)
npx serve .
```

Then open `http://localhost:8080`.

> **Note:** Opening the HTML files directly from the filesystem (`file://`) also works — all assets use relative paths.
