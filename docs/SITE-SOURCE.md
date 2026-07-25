# Retrieval Intelligence site source

The static project site is published from this `docs/` directory.

## Source and evidence boundary

The site describes the public contest edition contained in this repository. Product claims are derived from:

- `skills/retrieval-intelligence/SKILL.md`;
- `skills/retrieval-intelligence/references/retrieval-doctrine.md`;
- `skills/retrieval-reviewer/SKILL.md`;
- the deterministic local retrieval and evaluation scripts included with the two skills.

The site does not claim that retrieval proves source truth, that the baseline engine performs semantic or vector search, that every host can install this repository independently, or that the included reviewer authorizes consequential decisions.

## Files

- `index.html` — semantic single-page project overview;
- `style.css` — responsive presentation and accessibility treatment;
- `assets/retrieval-intelligence-hero.png` — generated 1600×900 raster hero artwork;
- `.nojekyll` — direct static-file serving marker.

## Deployment

`.github/workflows/deploy-pages.yml` uploads this directory with GitHub's official Pages Actions. Repository Pages must be configured to use **GitHub Actions** before the first deployment can publish.

## Review notes

The page uses one H1, semantic landmarks, a skip link, visible keyboard focus, descriptive links, meaningful alternative text, responsive layout, and reduced-motion handling. These checks support structural accessibility only; they are not a claim of formal accessibility conformance or representative-user success.
