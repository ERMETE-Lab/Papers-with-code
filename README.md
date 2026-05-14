# Papers with code

This repository is a lightweight wrapper for journal papers that link to code
hosted in other repositories in the `ERMETE-Lab` organization.

## Repository layout

- `index.html` renders a simple browser-based index of papers and linked code
  repositories.
- `papers.json` stores the paper metadata that drives the index.
- `repositories/` is reserved for the git submodules that mirror the linked
  repositories inside this wrapper repository.

## Adding a paper entry

1. Add the target repository as a git submodule under `repositories/<name>`.
2. Add a matching entry to `papers.json` with:
   - `title`
   - `repository`
   - `repository_url`
   - `submodule_path`
   - optional `authors`, `journal`, `year`, `doi`, `paper_url`, and `notes`

Until entries are added, the wrapper renders an empty-state message instead of
an empty table.

## GitHub Pages

The repository includes a workflow that publishes the static site (`index.html`
and `papers.json`) to GitHub Pages on pushes to `main`.
