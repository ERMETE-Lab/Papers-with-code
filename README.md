# Papers with code — ERMETE-Lab

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Browse%20paper%20index-blue?logo=github)](https://ermete-lab.github.io/Papers-with-code/)

This repository is a lightweight wrapper that indexes journal papers published by
the [ERMETE-Lab](https://github.com/ERMETE-Lab) group **that have companion
code** — not every group paper, only those accompanied by a public code
repository.

Each entry in the index links out to a dedicated repository in the ERMETE-Lab
organization. Those repositories are also tracked as git submodules under
`repositories/` so the code can be fetched alongside this wrapper in one step.

---

## Repository layout

| Path                   | Purpose                                                  |
| ---------------------- | -------------------------------------------------------- |
| `index.html`           | Static browser-based paper index (the GitHub Pages site) |
| `papers.json`          | Paper metadata that drives the index                     |
| `repositories/<name>/` | Git submodules — one per companion code repository       |

---

## Adding a new paper

### 1. Add the companion repository as a submodule

```bash
git submodule add https://github.com/ERMETE-Lab/<repo-name> repositories/<repo-name>
git commit -m "Add <repo-name> submodule"
```

Replace `<repo-name>` with the repository name in the ERMETE-Lab organization
(e.g. `NuSHRED`).

### 2. Add an entry to `papers.json`

Open `papers.json` and append a new object inside the `"papers"` array:

```jsonc
{
  "title": "Full paper title",
  "authors": "Author One; Author Two; Author Three",
  "journal": "Journal Name",
  "year": 2025,
  "volume": "1",           // optional
  "pages": "100000",       // optional
  "repository": "<repo-name>",
  "repository_url": "https://github.com/ERMETE-Lab/<repo-name>",
  "submodule_path": "repositories/<repo-name>",
  "doi": "10.xxxx/xxxxx",  // optional
  "paper_url": "https://doi.org/10.xxxx/xxxxx", // optional
  "notes": "One-sentence summary shown in the index." // optional
}
```

Required fields: `title`, `repository`, `repository_url`, `submodule_path`.

### 3. Push — the site updates automatically

A GitHub Actions workflow publishes `index.html` and `papers.json` to GitHub
Pages on every push to `main`. Once the workflow completes the new paper will
appear at
[ermete-lab.github.io/Papers-with-code](https://ermete-lab.github.io/Papers-with-code/).

---

## Cloning with submodules

To clone this repository and also fetch all companion code repositories in one
command:

```bash
git clone --recurse-submodules https://github.com/ERMETE-Lab/Papers-with-code.git
```

If you already cloned without `--recurse-submodules`:

```bash
git submodule update --init --recursive
```
