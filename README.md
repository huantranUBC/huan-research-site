# huan-research-site

Personal academic portfolio website for Huan M. Tran, built with
[Quarto](https://quarto.org) and published to GitHub Pages.

## Local preview

```bash
quarto preview
```

Opens a live-reloading preview in the browser. Edit any `.qmd` file and the page
updates automatically.

## Structure

| File | Purpose |
|---|---|
| `_quarto.yml` | Site config, navbar, theme |
| `index.qmd` | Home / bio |
| `publications.qmd` | Publications list (verified entries only) |
| `projects.qmd` | Research summaries (public-safe) |
| `cv.qmd` | Curriculum vitae |
| `styles.css` | Custom styling |
| `assets/` | Images, PDF CV |
| `.github/workflows/publish.yml` | Auto-render + deploy on push to `main` |

## Deployment

Pushing to `main` triggers a GitHub Action that renders the site and publishes
it to the `gh-pages` branch. In repo **Settings → Pages**, set the source to the
`gh-pages` branch.

## Notes

- `TODO` markers in the `.qmd` files flag items to confirm (ORCID, Scholar,
  dates, photo).
- The `.gitignore` blocks all data files — never commit restricted research data.
