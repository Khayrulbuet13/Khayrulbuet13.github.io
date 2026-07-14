---
name: add-paper
description: Add the next paper entry to the website from a PDF. Use when the user wants to add a new paper/publication to the site. Verifies the PDF is the author-accepted version, extracts metadata, scaffolds the next content/papers/paperN/, serves with hugo serve -D, and visually QAs the result.
---

# Add Paper

Append the next `content/papers/paperN/` entry from a paper PDF, matching the structure of the 13+ existing entries exactly. Each run auto-detects the next N — never overwrite an existing paper directory.

All scratch files (screenshots, downloaded BibTeX, temp conversions) go to `/tmp`, never the workspace.

## Phase 1 — Gather inputs

Ask the user for:

1. **PDF path** (required) — the paper PDF to add.
2. **DOI or journal URL** (optional) — will be extracted from the PDF if present.
3. **Cover figure image** (optional) — an image file for the cover. Existing covers are paper figures, not title pages. If the user skips this, fall back to rendering PDF page 1 (Phase 5).

## Phase 2 — Compliance gate

The site must only host versions the author may legally share. Read pages 1–2 of the PDF with the Read tool and check:

1. **Authorship** — "Khayrul Islam" appears in the author list.
2. **Version** — look for Version-of-Record (publisher-typeset) markers:
   - Publisher logo/branding, journal header/footer with volume/issue/page numbers
   - "Downloaded from …", "© <year> <publisher>" copyright lines, "Cite this: …" boxes
   - Final typeset multi-column publisher layout
   
   vs. accepted-manuscript markers: plain manuscript formatting, line numbers, "Accepted Manuscript" watermark, preprint styling.

Report a short **evidence list** of what was seen (never a silent pass):

- Both checks clean → state the evidence and proceed.
- Authorship fails → stop, ask the user to confirm this is their paper.
- VoR suspected → stop, show the evidence, and ask the user to explicitly confirm they have the right to post it (e.g., open-access CC-BY license, publisher policy). Proceed only on explicit confirmation.

## Phase 3 — Extract metadata from the PDF

Read as many pages as needed. Extract:

- **title** — exact
- **authors** — full list, in order, full names
- **abstract** — verbatim
- **tags** — from keywords + topics; Title Case; prefer reusing existing tags (`grep -h '^tags:' content/papers/*/index.md | tr ',' '\n'` to see them)
- **journal name** and **DOI**
- **date** — publication date (fall back to acceptance date, then year with a sensible month)
- **description** — one sentence, meta description; see *Tone* below
- **summary** — 1–2 sentences shown on the papers list; see *Tone* below
- **key highlights** — 4–6 bullets of the main contributions, each `**Label**: sentence`; see *Tone* below
- **affiliations** — numbered list, deduplicated
- **acknowledgments** — funding sources, one line
- optional links found in the paper: GitHub repo, dataset, arXiv id, supplementary materials

### Tone for description / summary / key highlights

The Abstract stays verbatim — full academic register, exactly as published. But `description`, `summary`, and Key Highlights are what a general visitor reads first (papers list, social share previews, search results), so write these like a blog post, not a journal submission:

- Audience: a curious non-specialist — a friend, a recruiter, a journalist — not a peer reviewer.
- Lead with why it matters or what's surprising, not the method name.
- Spell out or gloss jargon/acronyms on first use (e.g. "FPGA (a reprogrammable chip)", not bare "FPGA").
- Short, plain sentences, active voice. Unpack stacked noun-phrases ("teacher-student knowledge-distillation framework" → "a smaller AI model trained to mimic a bigger one").
- Stay factual and accessible, not hype — no clickbait, no exclamation points, no overselling.

## Phase 4 — Enrich via DOI

If a DOI is known:

```bash
curl -sL -H "Accept: application/x-bibtex" "https://doi.org/<DOI>"
```

- Use the returned BibTeX as the authoritative citation (clean up entry key to `<lastname><year><firstword>` style, e.g. `islam2025realtime`).
- Cross-check title/authors/year against Phase 3 extraction; flag mismatches.
- `editPost.URL` = publisher landing page (resolve the DOI or use the URL from the BibTeX); `editPost.Text` = journal name.

If the lookup fails or there is no DOI (preprint): build the BibTeX by hand from extracted metadata and ask the user for the canonical URL (journal/arXiv).

Also build a Chicago-style citation line (see existing papers for the format).

## Phase 5 — Scaffold the next paperN

1. Next N:
   ```bash
   ls content/papers | grep -E '^paper[0-9]+$' | sed 's/paper//' | sort -n | tail -1
   ```
   N = that + 1. The target `content/papers/paperN/` must not already exist.
2. `mkdir -p content/papers/paperN`
3. Copy the PDF → `content/papers/paperN/paperN.pdf`
4. Cover → `content/papers/paperN/paperN.png`:
   - User-provided figure: convert to PNG if needed — `sips -s format png <img> --out .../paperN.png`
   - Fallback: render PDF page 1 — `sips -s format png <pdf> --out .../paperN.png` (sips renders only the first page; that is the fallback cover)
5. Write `index.md` from `references/template.md`, filling every placeholder. Rules:
   - Front-matter keys and shape must match the template exactly (all 13 existing papers share it) — PaperMod needs `cover.relative: true` and `editPost` for the journal button.
   - `##### Download` links: `+ [Paper](paperN.pdf)` for the local copy, plus external Paper/Supplementary/arXiv/GitHub/Dataset links when known.
   - Drop optional sections that have no content (marked in the template). Never invent content — omit instead.

## Phase 6 — Serve

1. If something already answers on port 1313 (`curl -s http://localhost:1313 >/dev/null`), reuse it if it is this site's hugo server; otherwise kill the stale process (`lsof -ti :1313 | xargs kill`) first.
2. Start in background: `hugo serve -D`
3. Smoke check: `curl -s http://localhost:1313/papers/paperN/ | grep -io '<title>[^<]*'` returns the paper title.

## Phase 7 — Visual QA

Screenshot with headless Chrome (to `/tmp`):

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu \
  --screenshot=/tmp/qa-papers-list.png --window-size=1440,2400 http://localhost:1313/papers/
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu \
  --screenshot=/tmp/qa-paperN.png --window-size=1440,3200 http://localhost:1313/papers/paperN/
```

Read both PNGs and verify:

- Papers list: new entry appears at the correct position (sorted by date), cover thumbnail renders, title + summary correct.
- Entry page: cover image renders (no broken-image icon), title/date/authors correct, journal button (editPost) present, Download links listed, abstract justified, BibTeX code block renders, no layout breakage.

Anything wrong → fix `index.md`/assets → re-screenshot → re-check, until clean.

## Report

Finish with a short summary:

- Compliance evidence (what the gate saw)
- Files created under `content/papers/paperN/`
- Review URL: `http://localhost:1313/papers/paperN/`
- Anything the user should double-check (e.g., fallback cover used, missing supplementary link)

Do not commit — leave review and commit to the user.
