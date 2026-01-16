# Research Project Folder Structure (Recommended)

This guide outlines a simple, robust folder structure for applied economics research projects. The goal is to make projects:

- **Reproducible** (a new RA can run the project without guesswork)
- **Auditable** (clear provenance from raw inputs to final outputs)
- **Collaborative** (multiple people can work without stepping on each other)
- **AI-friendly** (a consistent place to store prompts, plans, and assistant rules)

I use (and recommend) a structure close to what many empirical research teams adopt, with a small number of conventions that tend to pay off quickly.

**Author:** [Peter John Lambert](mailto:p.j.lambert@lse.ac.uk), London School of Economics

---

## The Structure

Create a project folder (e.g., `my-paper/`) and inside it create the following directories:

```
my-paper/
  raw_data/
  aux_data/
  int_data/
  scripts/
  manuscript/
    tables/
    figures/
  context/
```

### `raw_data/`

**What goes here:** the original raw data from which all other results are obtained.

**Rules of thumb:**

- Treat this folder as **read-only**.
- Never overwrite raw data. If the provider updates the data, add a new dated file or versioned subfolder.
- Keep a small `README.md` or `data_source.txt` inside `raw_data/` describing:
  - where the data came from (URL, provider)
  - the date downloaded
  - any access restrictions / licences
  - a checksum (optional but great practice)

**Examples:**

- downloaded administrative microdata extracts
- original survey data files (Stata `.dta`, CSV, Parquet, etc.)
- PDF documentation supplied by the provider

---

### `aux_data/`

**What goes here:** small, original “support” datasets that are not the main raw data, but are needed for cleaning / joining / interpretation.

**Examples:**

- lookups and crosswalks (e.g., NAICS ↔ SIC, postcode ↔ region)
- code definitions (e.g., industry code descriptions)
- small external reference tables (CPI series, deflators, exchange rates)

**Why separate from raw data?**

Because these are often *hand-curated* and you may update them occasionally—whereas `raw_data/` should be immutable.

---

### `int_data/`

**What goes here:** any intermediate or final datasets derived in this project.

This is where your scripts should write outputs that can be regenerated from `raw_data/` + `aux_data/` + code.

**Examples:**

- cleaned datasets (e.g., `panel_clean.parquet`)
- intermediate merges
- model-ready datasets
- cached results that speed up iteration

**Suggested conventions:**

- Consider subfolders like:
  - `int_data/clean/`
  - `int_data/derived/`
  - `int_data/final/`
- Prefer non-proprietary, fast formats for large data (e.g., **Parquet**) where possible.

---

### `scripts/`

**What goes here:** all scripts that do the work.

**Typical substructure (optional but recommended):**

```
scripts/
  00_setup/
  01_ingest/
  02_clean/
  03_merge/
  04_analysis/
  05_tables_figures/
```

This mirrors the empirical workflow and makes it easy to run the project top-to-bottom.

**Naming tip:** prefix scripts with numbers so that sorting reflects execution order.

---

### `manuscript/`

**What goes here:** the paper itself, plus interim reports.

Inside `manuscript/`, create:

```
manuscript/
  tables/
  figures/
```

**Notes:**

- Treat `tables/` and `figures/` as (mostly) *generated outputs*.
- If you generate tables/figures from code, have scripts write them here.
- If you hand-edit a figure for slides/presentations, keep the editable source somewhere explicit (e.g., `manuscript/figures/source/`).

---

### `context/`

**What goes here:** project planning and AI assistant context.

This folder is deliberately separate from `scripts/` and `manuscript/`.

**Examples:**

- project plan / research notes
- variable dictionaries
- meeting notes
- “what I tried” logs
- prompt drafts
- assistant rules for **Cline / Claude Code / other AI tools**

**Recommended files:**

- `context/PROJECT_PLAN.md`
- `context/DATA_NOTES.md`
- `context/VARIABLE_DICTIONARY.md`
- `context/AI_RULES.md`

---

## A Minimal AI Rules Template (Cline / Claude Code)

Create a file like `context/AI_RULES.md` with something like:

```markdown
# AI Assistant Rules (Project)

## Ground truth
- The raw source data lives in `raw_data/` and must not be overwritten.
- Derived datasets must be written to `int_data/`.
- Tables and figures for the manuscript must be written to `manuscript/tables/` and `manuscript/figures/`.

## Reproducibility
- Prefer scripts that can run end-to-end.
- Avoid hard-coded absolute paths.
- Record assumptions and decisions in `context/`.

## Coding conventions
- Keep scripts modular.
- Use consistent naming.
- Write small README files in new directories if needed.
```

If your team uses a `.cursorrules`, `CLAUDE.md`, `cline.md`, or similar convention for tool-specific rules, put those files in `context/` as well and add links from `context/AI_RULES.md`.

---

## Practical Extras (Optional, but Useful)

Depending on your workflow, you may also add:

- `outputs/` (if you want a catch-all for non-manuscript outputs)
- `logs/` (pipeline logs)
- `config/` (API keys should **not** go here—use environment variables or secret managers)
- `environment/` (conda/pip lockfiles, `renv.lock`, `requirements.txt`, `Dockerfile`, etc.)

---

## Questions or Feedback?

- [Open an issue](https://github.com/Applied-Economics-With-AI/guides/issues) on our GitHub repository
- Contact: [Peter John Lambert](mailto:p.j.lambert@lse.ac.uk) at LSE

---

*Last updated: January 2026*

