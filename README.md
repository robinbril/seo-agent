# SEO Agent - Multi-site setup (Privé)

> SEO automatisering voor meerdere sites: Boomgaard&Munnik (hoofd), Auto Boomgaard, Robin Bril AI, REVIVE, Underground Royalty, Gardano.

---

## Status

**Boomgaard&Munnik (hoofdsite)**
- 7 regionale landingspagina's geschreven: Uithoorn, Amstelveen, Aalsmeer, De Kwakel, Kudelstaart, Nieuw-Vennep, Hoofddorp
- Content staat in `content/regionaal/`
- Competitive analysis gedaan: `briefs/competitive-analysis-2026-03-29.md`
- Geen rankings-data nog (baseline nog niet gedraaid)

**Overige sites (in `sites/`)**
- Auto Boomgaard: keyword-research.md aanwezig, 2 artikelen geschreven
- REVIVE: keyword-research.md aanwezig, 2 artikelen geschreven
- Robin Bril AI: keyword-research.md aanwezig, geen content nog
- Underground Royalty: keyword-research.md aanwezig, 1 artikel geschreven
- Gardano: keyword-research.md aanwezig, geen content nog

---

## Repo structuur

```
seo-agent/
├── scripts/                        # Python scripts (gedeeld door alle sites)
│   ├── keyword_gaps.py             # Keyword gap analyse via Brave Search
│   ├── scraper.py                  # Competitor pagina scraper
│   ├── rank_tracker.py             # Wekelijkse ranking tracker
│   ├── backlink_finder.py          # Vindt gastpost + backlink targets
│   ├── outreach_generator.py       # Schrijft outreach emails + gastblogs
│   ├── citation_builder.py         # Vindt lokale directory kansen
│   └── requirements.txt            # Python dependencies
│
├── sites/                          # Eén submap per site
│   ├── auto-boomgaard/             # autoboomgaard.nl (occasions)
│   ├── robin-bril/                 # robinbril.nl (AI agents)
│   ├── revive/                     # revive-skin.nl (skincare)
│   ├── underground-royalty/        # rickpeper.nl (kickboxen)
│   └── gardano/                    # christiaanwarner.nl (brand strategy)
│
├── content/
│   └── regionaal/                  # Regionale landingspagina's Boomgaard&Munnik
│
├── briefs/                         # Keyword analyses, competitor reports
├── rankings/                       # Wekelijkse ranking snapshots
├── config.json                     # Hoofd config: Boomgaard&Munnik
├── brand.md                        # Brand voice: Boomgaard&Munnik
└── CLAUDE.md                       # Instructies voor de AI agent
```

Elke site in `sites/` heeft:
- `config.json` — domein, concurrenten, keywords
- `brand.md` — brand voice en diensten
- `keyword-research.md` — keyword analyse en SEO rapport
- `content/` — gegenereerde artikelen
- `briefs/` — content briefs en analyses
- `rankings/` — ranking tracking

---

## Beschikbare sites

| Naam | Directory | Domein | Niche |
|---|---|---|---|
| Boomgaard&Munnik | *(root)* | boomgaard-site.vercel.app | Zakelijk vastgoed financiering |
| Auto Boomgaard | `sites/auto-boomgaard` | autoboomgaard.nl | Premium occasion dealer (Audi & Mercedes) |
| Robin Bril AI | `sites/robin-bril` | robinbril.nl | AI agents / digitale medewerkers |
| REVIVE | `sites/revive` | revive-skin.nl | GHK-Cu skincare serum |
| Underground Royalty | `sites/underground-royalty` | rickpeper.nl | Kickboxen 1-op-1 training Leiden |
| Gardano | `sites/gardano` | christiaanwarner.nl | Brand & Creative Strategist |

---

## Beschikbare commando's

Alle commando's werk je via Claude Code (`claude` in terminal vanuit deze map) of direct via de Python scripts.

### Keyword gap analyse

Via Claude Code:
```
Run keyword gap analysis
```

Via script (Boomgaard&Munnik):
```bash
python scripts/keyword_gaps.py
```

Via script (specifieke site):
```bash
python scripts/keyword_gaps.py --config sites/auto-boomgaard/config.json
```

Output: `briefs/keyword-gaps-YYYY-MM-DD.md`

---

### Competitor analyse

Via Claude Code:
```
Analyze competitor content for https://mogelijk.nl/zakelijk-vastgoed
```

Via script:
```bash
python scripts/scraper.py --url https://mogelijk.nl/zakelijk-vastgoed
```

Output: `briefs/competitor-mogelijk-YYYY-MM-DD.md`

---

### Artikel schrijven

Via Claude Code:
```
Write an article about zakelijk vastgoed financieren Uithoorn
```

Voor een andere site:
```
Write article for auto-boomgaard about Audi A6 occasion kopen Uithoorn
```

Output: `content/[slug].md` of `sites/[naam]/content/[slug].md`

---

### Rankings tracken

Via Claude Code:
```
Track rankings for all keywords
```

Via script:
```bash
python scripts/rank_tracker.py
```

Voor specifieke site:
```bash
python scripts/rank_tracker.py --config sites/revive/config.json
```

Output: `rankings/report-YYYY-MM-DD.md`

---

### Backlink kansen vinden

Via Claude Code:
```
Find backlink opportunities for boomgaard
```

Via script:
```bash
python scripts/backlink_finder.py --site boomgaard-site.vercel.app --niche "zakelijk vastgoed" --limit 20
```

Met concurrenten meegeven:
```bash
python scripts/backlink_finder.py --site boomgaard-site.vercel.app --niche "zakelijk vastgoed" --competitors mogelijk.nl,fortus.nl --limit 30
```

Output: `briefs/backlinks-YYYY-MM-DD.json`

---

### Outreach genereren

Via Claude Code:
```
Generate outreach for boomgaard targeting vastgoedpro.nl
```

Via script:
```bash
python scripts/outreach_generator.py --site boomgaard-site.vercel.app --target-url https://vastgoedpro.nl/blog --type guest-post
```

Output: `briefs/outreach-vastgoedpro-YYYY-MM-DD.md` (gastblog artikel + email)

---

### Lokale citations vinden

Via Claude Code:
```
Find citation opportunities for boomgaard in Uithoorn
```

Via script:
```bash
python scripts/citation_builder.py --site boomgaard-site.vercel.app --city Uithoorn
```

Voor meerdere steden:
```bash
python scripts/citation_builder.py --site boomgaard-site.vercel.app --city Amstelveen
python scripts/citation_builder.py --site boomgaard-site.vercel.app --city Aalsmeer
```

Output: `briefs/citations-Uithoorn-YYYY-MM-DD.md`

---

### Volledige SEO pipeline

Via Claude Code:
```
Run full SEO pipeline for boomgaard
```

Voert in volgorde uit:
1. Keyword gap analyse
2. Artikelen schrijven voor top-3 kansen
3. Backlink kansen vinden
4. Citation lijst genereren
5. Samenvatting rapport

---

## Backlink pipeline

Drie scripts werken samen voor backlink building:

```
[1] backlink_finder.py
    → Zoekt via Brave Search naar gastpost-kansen, resource pages,
      directories die relevant zijn voor jouw niche
    → Output: JSON met URL's, type (guest-post/resource/directory), relevantie
    │
    ▼
[2] outreach_generator.py
    → Neemt een URL uit de backlink lijst
    → Schrijft een volledig gastblog artikel + outreach email
    → Output: kant-en-klare tekst die je kunt sturen/insturen
    │
    ▼
[3] citation_builder.py (lokale variant)
    → Specifiek voor lokale directory vermeldingen
    → Output: lijst directories + NAP-template (Naam/Adres/Telefoon)
    → Gebruik ALTIJD exact dezelfde NAP data — inconsistentie schaadt local SEO
```

**NAP data Boomgaard&Munnik (kopieer letterlijk):**
```
Naam:    Boomgaard&Munnik
Adres:   Bruine Lijster 57, 1423 RV Uithoorn
Tel:     0297-820 200
Email:   info@boomgaardfinancieel.nl
Website: boomgaard-site.vercel.app
```

---

## Content strategie

**Aanpak: regionale landingspagina's + Amstelland focus**

Boomgaard&Munnik is gevestigd in Uithoorn. De nationale keywords ("zakelijk vastgoed financieren") hebben hoge concurrentie van grote partijen (Rabobank, ABN AMRO, mogelijk.nl). De strategie: win eerst de lokale keywords, bouw van daaruit autoriteit op.

**Fase 1 — Lokale keywords (nu actief)**
Eén landingspagina per stad in de regio Amstelland:
- Uithoorn ✓
- Amstelveen ✓
- Aalsmeer ✓
- De Kwakel ✓
- Kudelstaart ✓
- Nieuw-Vennep ✓
- Hoofddorp ✓

Nog te schrijven: Abcoude, De Ronde Venen, Amsterdam Zuidoost, Alphen aan den Rijn

**Fase 2 — Nationale nichemarkten**
Keywords met middelhoge concurrentie die aansluiten op diensten:
- "zakelijke hypotheek aanvragen" (artikel live: `sites/auto-boomgaard/content/`)
- "herfinanciering zakelijk vastgoed"
- "vastgoed financieren zonder bank"
- "second opinion hypotheek zakelijk"

**Structuur per artikel:**
- Titel met stad/regio in H1
- 800–1200 woorden
- FAQ sectie (5–8 vragen) voor featured snippets
- Interne links naar andere regionale pagina's
- CTA: afspraak maken via contactformulier

---

## Wekelijkse workflow

Voer dit elke maandag uit, in deze volgorde:

**Stap 1 — Rankings tracken (5 min)**
```bash
python scripts/rank_tracker.py
```
Of via Claude Code: `Track rankings for all keywords`

Open `rankings/report-YYYY-MM-DD.md` en bekijk welke keywords zijn gestegen of gedaald.

**Stap 2 — Nieuwe content (30–60 min)**

Schrijf 2–3 nieuwe artikelen op basis van de keyword gap analyse.

Via Claude Code:
```
Write an article about [keyword uit keyword-gaps brief]
```

Plak de gegenereerde content op de website.

**Stap 3 — Backlinks (15 min)**

Controleer `briefs/backlinks-*.json` op nieuwe kansen.
Stuur 2–3 outreach emails per week. Gebruik:
```bash
python scripts/outreach_generator.py --site boomgaard-site.vercel.app --target-url [URL] --type guest-post
```

**Stap 4 — Citations (10 min, eerste 4 weken intensief)**

Voeg je aan 2–3 directories toe per week. Focus eerst op:
- Google Business Profile (verplicht)
- KvK-vermelding
- Thuisadres.nl
- Gouden Gids
- Lokale gemeentegidsen

**Stap 5 — Keyword gap check (1x per 2 weken)**
```
Run keyword gap analysis
```
Kijkt of er nieuwe kansen zijn bijgekomen.

---

## Environment instellen

Scripts hebben `BRAVE_API_KEY` nodig.

**PowerShell (tijdelijk):**
```powershell
$env:BRAVE_API_KEY = "jouw_key_hier"
```

**PowerShell (permanent via profiel):**
```powershell
Add-Content $PROFILE "`n`$env:BRAVE_API_KEY = 'jouw_key_hier'"
```

**Optioneel — voor AI outreach:**
```powershell
$env:ANTHROPIC_API_KEY = "jouw_key_hier"
```

API key aanmaken: [brave.com/search/api](https://brave.com/search/api/) (gratis, 2.000 queries/maand)
