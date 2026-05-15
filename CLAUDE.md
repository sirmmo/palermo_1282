# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A bilingual (IT/EN) LaTeX project: *Vespri 1282*, a one-shot Forged in the Dark
tabletop RPG module set in Palermo, February–March 1282. Not software — the
"build" produces PDFs. Content is historically grounded (see `nomi_personaggi.tex`
header for the onomastic/chronicle sources).

## Build

Requires **XeLaTeX** (TeX Live 2022+). Fonts: EB Garamond, Cinzel, Cinzel
Decorative. Double compilation is required for the ToC and internal references.

```bash
cd it && xelatex main_it.tex && xelatex main_it.tex   # Italian manual
cd en && xelatex main_en.tex && xelatex main_en.tex   # English manual
xelatex schede_vespri.tex && xelatex schede_vespri.tex # character sheets (from root)
```

`main_it.tex` / `main_en.tex` must be compiled *from inside* their own
directory — they `\input` siblings by relative path (`preamble_it`,
`sections/...`) and reach shared files via `../shared/`.

## Architecture

Three-way split designed so the two language editions never duplicate
invariant content:

- **`shared/`** — language-agnostic files `\input` by both editions.
  - `preamble_shared.tex` is the single source of truth for all visual
    design: fonts, the `oro`/`pergamena`/`bordoscuro` color palette, page
    geometry, chapter/section title formats, and the custom content
    commands (see below).
  - `app_rpgschema.tex`, `app_ohm.tex` — RDF/Turtle appendices, identical
    in both editions.
- **`it/`** and **`en/`** — one directory per edition. Each has a thin
  `main_*.tex` (cover + `\part`/`\input` structure only) and a
  `preamble_*.tex` that sets `polyglossia` language, localizes the four
  playbook attribute labels (`\PlaybookAttrA..D`), loads `hyperref`, then
  `\input`s `preamble_shared.tex`. Section files `sections/01_*..08_*.tex`
  mirror each other 1:1 across languages — **a structural change in one
  edition almost always needs the mirror change in the other.** The EN
  edition has one extra appendix (`glossary.tex`).
- **`schede_vespri.tex`** — standalone `article` (not `memoir`), compiled
  from the repo root. It re-declares its own fonts/colors and does **not**
  share `preamble_shared.tex`; the palette is duplicated here, so a color
  change must be applied in both places.
- **`nomi_personaggi.tex`** — standalone name registry for PCs/NPCs.

`main_*.tex` is `memoir` with `\part`s: *Il Contesto / Il Gioco / Public
History*, then `\appendix`. Note `08_passione` is `\input` before
`07_public_history` despite the filename order.

## Editing conventions

- Body content uses custom semantic commands from `preamble_shared.tex`
  rather than raw formatting: `\nota` (GM note box), `\regola` (rules box),
  `\citastorica` (historical quote), `\statblock` (NPC stat block),
  `\secsep` / `\filetto` / `\filettodoppio` (separators). Prefer these over
  ad-hoc `mdframed`/`rule` so the two editions stay visually consistent.
- Never hardcode colors — use the named palette (`oro`, `ororosso`,
  `pergamena`, `bordoscuro`, `testoscuro`, `grigionote`).
- Licensed CC BY-SA 4.0; an unofficial derivative of Forged in the Dark
  (John Harper / Evil Hat) — keep the non-affiliation notice intact.
