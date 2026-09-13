# pendletonian.com

Static personal site for Ian M. Pendleton, served by GitHub Pages from `ipendlet/ipendlet.github.io`.
No build step: edit the HTML, commit, push to `main`, and Pages redeploys in about a minute.

```
index.html                 home: WebGL constellation hero (three.js r128 from cdnjs)
cv/index.html              curriculum vitae
presentations/index.html   talks and posters
chemical-space/            landing page + two interactive visualizations
assets/site.css            shared styles
CNAME                      custom domain for GitHub Pages
.nojekyll                  serve files as-is (skip Jekyll)
```

Preview locally:

```bash
python3 -m http.server 8000
```

## One-time setup

1. **SSH key on GitHub.** Add `~/.ssh/id_ed25519.pub` at github.com → Settings → SSH and GPG keys.
2. **Create the repo** `ipendlet.github.io` (public, empty), then:
   ```bash
   git remote add origin git@github.com:ipendlet/ipendlet.github.io.git
   git push -u origin main
   ```
3. **Verify the domain** (prevents takeover): GitHub → Settings → Pages → *Add a verified domain* → add the TXT record it shows.
4. **DNS at Squarespace** (Domains → pendletonian.com → DNS):
   - Turn **off** domain forwarding for `pendletonian.com` and `www`.
   - Delete the Squarespace A/CNAME records for `@` and `www`.
   - Add:

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

   - **Keep** the Proton Mail records untouched: `MX 10 mail.protonmail.ch`, `MX 10 mailsec.protonmail.ch`,
     and the `protonmail-verification` TXT (plus any DKIM/SPF/DMARC records present).
5. **Enable HTTPS**: GitHub → repo Settings → Pages → custom domain `pendletonian.com` → wait for the
   certificate (minutes to ~1 hour after DNS propagates) → tick **Enforce HTTPS**.
6. Retire the WordPress.com site (ianpendleton.wordpress.com) once the new site is live, or point it here.
