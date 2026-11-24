# Egho Pratama – Resume

Personal resume website of **Egho Pratama**, a frontend-focused fullstack developer based in Jakarta, Indonesia.

🔗 **Live site:** https://eghopratama.github.io/egho-resume/

## Features

- One-page resume with sections for About, Education, Skills, Experience, Portfolio, Publications, and Contact.
- Adaptive navigation: fixed sidebar on desktop, tabbed layout on mobile.
- English and Indonesian language support.
- Downloadable resume (PDF) from the About section.
- Contact form powered by [EmailJS](https://www.emailjs.com/) (no backend needed).
- SEO basics: meta description, Open Graph / Twitter tags, JSON-LD, `robots.txt`, and `sitemap.xml`.

## Tech stack

Vue 3 (Composition API), Vite, Bootstrap 5, SCSS, Chart.js, Swiper, Font Awesome.

## Getting started

Requires Node.js 18 or newer (Node 22 is used in CI).

```bash
npm install
npm run dev      # start the dev server (http://localhost:5173/egho-resume/)
npm run build    # production build into dist/
npm run preview  # preview the production build locally
```

Note: the app is served under the `/egho-resume/` base path (see `base` in `vite.config.js`), so open the dev server at that path rather than at the root.

## Editing the content

All content lives in JSON files under `public/data/` – no code changes needed for day-to-day updates:

| File | What it controls |
|------|------------------|
| `profile.json` | Name, role, photo, contact options and social links |
| `settings.json` | Preloader and supported languages |
| `sections.json`, `categories.json` | Section titles, order, and navigation groups |
| `strings.json` | Shared UI labels (English and Indonesian) |
| `sections/*.json` | The content of each section (about, education, skills, experience, portfolio, publications, contact) |

Dates in the JSON files use **0-based months** (`"month": 0` is January, `"month": 10` is November). For a role that is still ongoing, use `"dateEnd": {"string": "now"}`.

The downloadable resume is `public/files/Septya_Egho_Pratama-Resume.pdf`. To update it, replace that file. The path is set by `resume_pdf_url` in `public/data/sections/about.json`.

More details on configuring the template are in [docs/CONFIGURATION.md](./docs/CONFIGURATION.md).

## Deployment

Pushing to `main` triggers the GitHub Actions workflow in `.github/workflows/deploy.yml`, which builds the site and publishes `dist/` to the `gh-pages` branch. In the repository settings, GitHub Pages should be set to deploy from the `gh-pages` branch. If you rename the repository or use a custom domain, update `base` in `vite.config.js`. See [docs/DEPLOYMENT.md](./docs/DEPLOYMENT.md) for more.

## Credits and license

This site is built on the [Vue Resume Template](https://github.com/ryanbalieiro/vue-resume-template) by [Ryan Balieiro](https://ryanbalieiro.com/), which is released under the MIT license. The design credit in the site footer is kept intentionally. See the upstream repository for the original license text.

Built with [Vue](https://vuejs.org/), [Bootstrap](https://getbootstrap.com/), and [Font Awesome](https://fontawesome.com/).
