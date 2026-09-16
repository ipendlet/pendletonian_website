# pendletonian.com

Static personal site for Ian M. Pendleton, served by GitHub Pages from
[`ipendlet/pendletonian_website`](https://github.com/ipendlet/pendletonian_website) (branch `main`, root folder).
There is no build step: edit the HTML/CSS, commit, push to `main`, and Pages redeploys in about a minute.

```
index.html                         home: hero, "Who am I?", links
cv/index.html                      curriculum vitae
presentations/index.html           talks and posters
chemical-space/index.html          landing page for the visualizations
chemical-space/constellation.html  interactive 3D atlas (three.js r128 via cdnjs)
chemical-space/explore.html        animated story (canvas 2D)
assets/site.css                    shared styles
assets/indian-creek.jpg            homepage photo
CNAME                              custom domain for GitHub Pages
.nojekyll                          serve files as-is (skip Jekyll)
```

## View locally

Serve the folder over HTTP rather than opening files directly. Links like `cv/` resolve to
`cv/index.html` only through a server, and browsers restrict some features on `file://` pages.

```bash
cd ~/PycharmProjects/pendletonian_website
python3 -m http.server 8000 --bind 127.0.0.1
```

Then open <http://localhost:8000>. Stop the server with `Ctrl+C`.

- **Seeing an old version?** The server sends no cache headers, so hard-refresh with `Ctrl+Shift+R`.
- **From PyCharm:** right-click `index.html` → *Open In* → *Browser*. PyCharm's built-in server works too,
  but it serves under `/pendletonian_website/`, so check links with the Python server before pushing.
- **Needs internet:** three.js loads from cdnjs and fonts from Google Fonts. Offline, the hero falls back
  to a plain gradient and text uses system fonts.
- **Phone preview on the same Wi-Fi:** bind to all interfaces with `python3 -m http.server 8000`
  and browse to `http://<this-machine's-LAN-IP>:8000`. Stop it when done, since it exposes the folder to your network.

## Publish a change

```bash
git add -A
git commit -m "Describe the change"
git push
```

Check progress under the repo's **Actions** tab (the "pages build and deployment" workflow).
The repo is public, so everything committed, including history, is visible to anyone.

## Hosting configuration (reference)

- **Pages source:** repo Settings → Pages → *Deploy from a branch* → `main` / `(root)`.
- **Custom domain:** `pendletonian.com` (set by the `CNAME` file). The domain is registered at Squarespace, and DNS is managed there.
- **GitHub Pages DNS records:**

  | Type  | Host | Value |
  |-------|------|-------|
  | A     | @    | 185.199.108.153 |
  | A     | @    | 185.199.109.153 |
  | A     | @    | 185.199.110.153 |
  | A     | @    | 185.199.111.153 |
  | AAAA  | @    | 2606:50c0:8000::153 |
  | AAAA  | @    | 2606:50c0:8001::153 |
  | AAAA  | @    | 2606:50c0:8002::153 |
  | AAAA  | @    | 2606:50c0:8003::153 |
  | CNAME | www  | ipendlet.github.io |

  The `www` CNAME points at `ipendlet.github.io` (the account's Pages host), not at the repo name.
- **Email:** Proton Mail. Never remove `MX 10 mail.protonmail.ch`, `MX 10 mailsec.protonmail.ch`,
  the `protonmail-verification` TXT record, or any DKIM/SPF/DMARC records.
- **HTTPS:** a certificate issued by GitHub, with *Enforce HTTPS* on under repo Settings → Pages.

## Content notes

- Employer-specific figures and names are deliberately generalized in the chemical-space
  visualizations (orders of magnitude only). Keep them that way.
- The phone number is intentionally not published. The email is written as `ian ~at~ pendletonian.com`.
