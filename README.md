# Vespri 1282 — Pacchetto Completo

One-shot Forged in the Dark bilingue (IT/EN) · 4 tavoli · 28–35 giocatori  
Palermo, febbraio–marzo 1282

## Struttura

```
vespri1282/
├── it/                          ← Versione italiana
│   ├── main_it.tex              → xelatex main_it.tex
│   ├── preamble_it.tex
│   └── sections/
│       ├── 01_storica.tex       Contestualizzazione storica (~10pp)
│       ├── 02_regole.tex        Regole FitD adattate
│       ├── 03_fazioni.tex       Le 4 fazioni
│       ├── 04_playbook.tex      32 playbook (8×4)
│       ├── 05_npc.tex           NPC storici con stat block
│       ├── 06_esiti.tex         Sistema punteggi 0–16
│       ├── 07_public_history.tex Guida uso scolastico (licei)
│       ├── 08_passione.tex      Layer PdlP — Ruoli Passionali
│       └── appendici/
│           └── app_storica.tex  Cronologia + storiografia
│
├── en/                          ← English version
│   ├── main_en.tex              → xelatex main_en.tex
│   ├── preamble_en.tex
│   └── sections/
│       ├── 01–08 *.tex          (mirror IT, full English)
│       └── appendici/
│           ├── app_storica.tex  Chronology + historiography
│           └── glossary.tex     Glossary of historical terms
│
├── shared/                      ← File invarianti (usati da entrambi)
│   ├── preamble_shared.tex      Font, colori, comandi comuni
│   ├── app_rpgschema.tex        RDF/Turtle — rpg-schema.org
│   └── app_ohm.tex              RDF/Turtle — OpenHistoryMap
│
└── schede_vespri.tex            28 schede personaggio A4
```

## Compilazione

```bash
# Versione italiana
cd it && xelatex main_it.tex && xelatex main_it.tex

# Versione inglese
cd en && xelatex main_en.tex && xelatex main_en.tex

# Schede personaggio (dalla root)
xelatex schede_vespri.tex && xelatex schede_vespri.tex
```

> Doppia compilazione necessaria per indice e riferimenti interni.

## Requisiti

- **XeLaTeX** (TeX Live 2022+ o MiKTeX recente)
- **Font**: EB Garamond, Cinzel, Cinzel Decorative (Google Fonts)
- **Pacchetti**: pgfornament, mdframed, lettrine, GoudyIn, geometry,
  fancyhdr, titlesec, xcolor, tikz, booktabs, enumitem, multicol,
  polyglossia, microtype, fontspec, csquotes

## Contenuto

| Sezione | IT | EN |
|---|---|---|
| Contestualizzazione storica | ✓ | ✓ |
| Regole FitD adattate | ✓ | ✓ |
| 4 fazioni con punteggi | ✓ | ✓ |
| 32 playbook tematici storici (8×fazione) | ✓ | ✓ |
| NPC storici (stat block) | ✓ | ✓ |
| Sistema esiti 0–16 | ✓ | ✓ |
| Guida public history (licei) | ✓ | ✓ |
| Layer Passionale (PdlP) | ✓ | ✓ |
| App. storica + storiografia | ✓ | ✓ |
| Glossario termini storici | — | ✓ |
| App. rpg-schema.org (RDF) | shared | shared |
| App. OpenHistoryMap (RDF) | shared | shared |
| 28 schede personaggio A4 | standalone | standalone |

## Crediti

- **Sistema**: Forged in the Dark — John Harper (Evil Hat Productions)
- **Layer Passionale**: ispirato a Pasión de las Pasiones — Brandon León-Gambetta
- **Dati geografici**: OpenHistoryMap — openhistorymap.org
- **Ontologia RPG**: rpg-schema.org
- **Licenza**: CC BY-SA 4.0

