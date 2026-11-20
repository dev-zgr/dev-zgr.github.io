# Hüseyin Özgür Kamalı - personal academic website

Source of https://dev-zgr.github.io, built with [Jekyll](https://jekyllrb.com) and the
[AcademicPages](https://github.com/academicpages/academicpages.github.io) template (a fork of Minimal Mistakes).
Every push to `main` builds the site with GitHub Actions and deploys it to GitHub Pages.

## Where to edit things

| What | File |
| --- | --- |
| Name, sidebar bio, location, email, GitHub, Google Scholar, ORCID, LinkedIn | `_config.yml` (`author:`) |
| Colors (menu red, link blue, notice box) as hex codes | `_config.yml` (`theme_colors:`) |
| Biography, notice box, research text and topics | `_data/home.yml` |
| News | `_data/news.yml` |
| Publications (grouped by year automatically) | `_data/publications.yml` |
| Top menu | `_data/navigation.yml` |
| Profile photo | `images/profile.jpg` |
| CV and paper PDFs | `files/` (the CV menu item opens `files/cv.pdf`) |

A sidebar line (for example Google Scholar or ORCID) is hidden while its value in `_config.yml` is empty.
Write the full URL to show it, e.g. `googlescholar: "https://scholar.google.com/citations?user=XXXX"`.

## Connecting a custom domain

1. Repository **Settings -> Pages -> Custom domain**: enter the domain (e.g. `ozgurkamali.com`) and save.
   GitHub adds the domain to the Pages settings; with the Actions deployment no `CNAME` file is needed.
2. At the domain registrar, add the DNS records:
   - apex domain (`ozgurkamali.com`): `A` records to `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
     (optionally `AAAA` to `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`)
   - `www` subdomain: `CNAME` to `dev-zgr.github.io`
3. When the DNS check passes, tick **Enforce HTTPS**.
4. Change `url` in `_config.yml` to the new address so links in search results and social previews use it.

## Local preview

With Docker (no local Ruby needed):

```bash
docker run --rm -v "$PWD":/app -w /app node:24-alpine npx -y uglify-js@3 assets/js/plugins/jquery.greedy-navigation.js assets/js/_main.js assets/js/theme.js -c -m -o assets/js/main.min.js
docker run --rm -p 4000:4000 -v "$PWD":/app -w /app ruby:3.1 sh -c "bundle install && bundle exec jekyll serve -H 0.0.0.0"
```

Then open http://localhost:4000.

## License

The theme code is MIT licensed (see `LICENSE`). The text, photo and PDFs are the author's own and are not covered by that license.
