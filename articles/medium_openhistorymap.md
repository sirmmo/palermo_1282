# Vespri 1282
## Playing the night Palermo refused to be Angevin — and why I built it on OpenHistoryMap

*Draft for the OpenHistoryMap Medium publication.*

---

On the evening of 30 March 1282, Palermo rose against its French rulers. Within a few hours, two thousand Angevin functionaries — soldiers, officials, civilians — were dead, and the political shape of the Mediterranean was about to change for the next two decades.

Historians still argue about what triggered it. Steven Runciman, in his still-influential 1958 book *The Sicilian Vespers*, presents the night as the explosive endpoint of an organised conspiracy, woven together by Giovanni da Procida with Aragonese gold and Byzantine intelligence. David Abulafia and Jean Dunbabin, more recently, have pushed back: yes the conspiracy existed, but the revolt itself was largely spontaneous, set off by an accumulated daily violence — the searches, the requisitions, the soldier who did not know when to stop. The current scholarly consensus is some braid of both. Most likely, the conspirators did not control the timing. Most likely, the people in Piazza Santo Spirito did not know there was a plan.

This question — *was the Vespers a plan, an explosion, or a coincidence between two things that were each insufficient on their own?* — is, for an OpenHistoryMap audience, a familiar shape. It is the question of whether a historical outcome can be reduced to a single agent, and how a *place* and a *moment* can hold together causes that operate on completely different timescales.

For the past few months I've been building a tabletop role-playing game that asks players to live inside that question — and to do so as a piece of digital public history rather than just a printed book.

[**Vespri 1282**](https://sirmmo.itch.io/vespri-1282) is a bilingual (Italian / English) Forged in the Dark one-shot designed for 3–4 GMs running 3–4 simultaneous tables of 6–8 players each — up to 32 people sharing the same six weeks of Palermo, the same 30 March they cannot see coming. It is published under CC BY-SA 4.0 at [github.com/sirmmo/palermo_1282](https://github.com/sirmmo/palermo_1282), and it ships with two interlocking RDF/Turtle appendices: one for OpenHistoryMap (the spatial-temporal layer), one for [rpg-schema.org](https://rpg-schema.org) (the semantic layer of the game itself). This article is partly a designer's note, partly a small case study in what happens when you treat a game module as an open-data artefact.

---

## Four tables, four readings of the same night

Players are distributed across four faction tables, each with its own GM:

- **I Congiurati** — Giovanni da Procida's network, *in medias res*. They know the most about what's coming, and they cannot tell anyone.
- **I Baroni Siciliani** — the Sicilian nobility, recruited mid-session, deciding which side to back.
- **Il Clero** — the Church: the symbols, the spaces of refuge, and the bells of Santo Spirito.
- **Il Popolo** — the artisans, the fishwives, the boys, the widows: those who will actually be in the square.

A fifth, *coordinating* GM tracks the per-faction scores (0–4 each, totalling 0–16) and pushes three timed "junction moments" across all tables: *La Voce* (rumour, ~45 minutes in), *La Crisi* (city-scale event, ~90 minutes), *Le Campane* (the procession is starting, ~150 minutes). Players at one table never directly see another table's actions — they receive only the consequences, filtered through their faction's perspective. The final outcome of the night is a single number against a fixed table of bands, but how that number was generated is a thirty-person collaborative argument about cause, agency, and complicity.

This is, structurally, a way of *playing* a particular historiographic intuition: **no single perspective produced the Vespers**. The conspirators believed they were running the timeline. The people believed it was their rage that lit the fuse. The clergy believed they had managed the symbols. The barons believed they were buying themselves an honourable position. All four are right and all four are wrong — and the scoring system makes that mathematically literal. The session can end with the Vespers entirely failing, with a partial uprising suppressed within days, with the historical Vespers landing more or less as recorded, or with a coordinated insurrection that breaks out *better* than history — but in every case, the players will have to reconstruct, in debriefing, *who did what to whom*.

For runs with only three GMs available, the manual provides a tested 0–12 rescaling and two named configurations: drop the Barons (Runciman-leaning: the conspiracy is on stage, the nobility is offstage pressure) or drop the Conspirators (Abulafia-leaning: no organised centre, only a society at the breaking point).

---

## OpenHistoryMap as ground truth

The spatial and temporal scaffolding of the module lives in `shared/app_ohm.tex` as Turtle:

```turtle
@prefix ohm:      <https://openhistorymap.org/ontology/> .
@prefix ohmplace: <https://openhistorymap.org/place/> .
@prefix v1282:    <https://openhistorymap.org/vespri1282/> .

v1282:period_1282 a ohm:HistoricalPeriod ;
  rdfs:label "Palermo 1282 — Vespri Siciliani"@it ,
             "Palermo 1282 — Sicilian Vespers"@en ;
  time:hasBeginning [ time:inXSDDate "1282-02-01"^^xsd:date ] ;
  time:hasEnd       [ time:inXSDDate "1282-03-31"^^xsd:date ] ;
  ohm:politicalContext "Dominio angioino"@it .

ohmplace:palermo_cassaro a ohm:HistoricalQuarter ;
  rdfs:label "Cassaro"@it , "Cassaro"@en ;
  dcterms:description
    "Centro storico di Palermo, sede del Palazzo dei Normanni."@it .
```

Each of the four quartieri (Cassaro, Kalsa, Seralcadio, Albergheria) and each of the significant locations (the Royal Palace, the Cathedral, the church of Santo Spirito outside the walls, the port where Charles of Anjou's fleet was being assembled) is encoded as a first-class entity, with cross-references to the surviving primary sources — Bartolomeo di Neocastro's *Historia Sicula*, Saba Malaspina's chronicle, the Aragonese chancery registers post-1282, the onomastic dictionary of Caracausi.

This matters for two reasons.

First, **the Palermo of the game is the same dataset another OpenHistoryMap project could query**. A future documentary visualisation, an interactive walking tour through the Albergheria, or a comparative study of Mediterranean port cities under foreign administration can pull the same IRIs. The game is not a closed parallel-universe Palermo; it sits in the same graph as the academic Palermo.

Second, **the GM and the player can verify**. A coordinator who wants to push a junction moment about "the Aragonese fleet sailing from Barcelona" can read the date directly from the Turtle, rather than trusting that I got it right when transcribing it into prose. The historical scaffolding is auditable.

---

## rpg-schema.org as the game-side graph

A parallel appendix uses rpg-schema.org with FitD extensions to encode the *game* itself: factions, the 32 playbooks, the historical NPCs, the action vocabulary, the trauma list, the scoring system, the outcome bands.

The pay-off is that each historical NPC gets identified twice. Alaimo da Lentini, the Sicilian baron whose position in 1282 was famously ambiguous, exists as a `fitd:StatBlock` (for use during play) and as an `ohm:HistoricalPerson` (with `dcterms:source` linking to the relevant entries in the chronicles). The two graphs share IRIs deliberately. A future researcher querying *who is Alaimo da Lentini* gets back a stat block and a primary source citation in the same response. A future tool — a character-sheet generator, a translation pipeline, a campaign visualiser — can walk the same graph instead of re-parsing the manual.

---

## Bilingual public history, on purpose

The Sicilian Vespers are remembered very differently inside and outside Italy. In nineteenth-century Italian nationalist historiography they were a *Risorgimento avant la lettre*: a brave people throwing off the foreign yoke. In Anglophone historiography — most influentially in Runciman — they are a Mediterranean grand-strategy moment, Sicily as the chess square where Aragonese, Byzantine and Angevin ambitions collide. Neither reading is wrong. Both are partial.

Putting the same module in both languages, with the same primary sources cited and the same Turtle layer behind it, is a small but deliberate gesture against the idea that "Italian history" and "European history" should live in different cabinets. The build pipeline produces `vespri_1282_it.pdf` and `vespri_1282_en.pdf` from the same source tree on every push, with a shared preamble, shared semantic appendices, and language-aware chapter switches. They are versions of one artefact, not translations of two.

The classroom appendix (`07_public_history`) makes the educational use explicit: a structured 4-hour adaptation for *licei classici/scientifici*, with debriefing protocol (de-roll, historical reflection, contemporary connections) and three written-assignment options — a character diary, a historiographic analysis of the Runciman/Abulafia debate from the player's lived experience, or a counter-chronicle from a non-Villani perspective (a Sicilian friar, a Genoese merchant, an Angevin survivor). It maps explicitly to the Indicazioni Nazionali for the *licei*. The aim is for a student to leave the session unable to read a chronicle the same way again — having spent three hours being one of the people who had to choose.

---

## Two design notes worth flagging

Two mechanics are worth a paragraph each, because they're attempts to make political history feel structurally entangled with personal history.

**The Passione layer** (chapter 8), inspired by Brandon León-Gambetta's *Pasión de las Pasiones*, is an optional dramatic overlay activated per table. Each character can adopt one of eight Passion Roles — the Protagonist, the Impossible Love, the Betrayer, the Parental Figure, the Rival, the Innocent Bystander, the Martyr, the Redeemed — with an emotional resource track (Passione, 5 boxes), gain and spend mechanics, and a *guaranteed* dramatic moment before the session ends. It exists because the Baron who must choose between his cause and his son is a stronger character than the Baron choosing between two strategies. The political game is more interesting when it is hostage to a personal one.

**Legare e Sciogliere**, the Clergy's signature action ("to bind and to loose," from Matthew 16:19), translates a piece of Catholic political theology directly into a player-facing rule. A Clergy character with a Passion Role can, once per act, spend 2 Passione to *forge* a new Connection between two other characters (PCs or NPCs), or 3 Passione to *break* one. The targets cannot refuse the bond, but they choose its nature — love, debt, blood, shared secret. The Church of 1282 Sicily exercised power not military but *relational*; the mechanic lets that power be wielded — and resented — by the table.

---

## Why open, and why now

Everything in the project is CC BY-SA 4.0. The source is in a public GitHub repository with a reproducible CI/CD pipeline (XeLaTeX in TeX Live 2026, building four PDFs on every release and pushing them to itch.io on tagged releases). The OpenHistoryMap and rpg-schema.org appendices are queryable Turtle, not pictures of Turtle. The shared LaTeX preamble has an edition-aware switch so the same shared appendices render in either language without code duplication.

This is partly personal preference and partly an OpenHistoryMap principle: **historical artefacts that depend on a single distributor, or a single rendering of their data, become brittle**. Twenty years from now I want some GM in a town I have never visited to be able to fork this module, swap Palermo for somewhere else with the same structural tensions — Bruges 1302, Catalan Barcelona 1640, anywhere a city had to decide whether to refuse its rulers — and rebuild the experience with the same scaffolding. The game is, in this sense, an argument for what an open historical artefact can be: not a fixed text, but a structured invitation to keep asking the question.

*Vespri 1282* will be played for the first time at Mensa Italia Games, Palermo, 4–7 June 2026. After that, the four tables will close, the bells of Santo Spirito will fall silent, and the manual will keep waiting on itch.io for the next four people who want to try.

---

**Resources**
- Source & PDFs: [github.com/sirmmo/palermo_1282](https://github.com/sirmmo/palermo_1282)
- Itch.io: [sirmmo.itch.io/vespri-1282](https://sirmmo.itch.io/vespri-1282)
- OpenHistoryMap: [openhistorymap.org](https://openhistorymap.org)
- rpg-schema.org: [rpg-schema.org](https://rpg-schema.org)
- Forged in the Dark / Blades in the Dark: John Harper, Evil Hat Productions
- *Pasión de las Pasiones*: Brandon León-Gambetta

**Cited historiography**
- Steven Runciman, *The Sicilian Vespers* (1958)
- David Abulafia, *The Two Italies* and later essays
- Jean Dunbabin, *Charles I of Anjou: Power, Kingship and State-Making in Thirteenth-Century Europe* (1998)
- Giovanni Villani, *Nuova Cronica* (XIV sec.)
- Bartolomeo di Neocastro, *Historia Sicula*
