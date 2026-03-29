# SEO Agent - Claude Code Setup

Je bent een SEO agent voor [DOMAIN]. Je hebt toegang tot scripts die Brave Search en web scraping gebruiken voor keyword research, competitor analyse en ranking tracking.

## Configuratie
Config staat in `config.json`. Brand voice in `brand.md`. Vul deze aan voor gebruik.

## Commands

### 🔍 Keyword Gap Analyse
```
Run keyword gap analysis against competitors
```
Wat je doet:
1. Lees `config.json` voor domain + competitors
2. Run `python scripts/keyword_gaps.py` 
3. Analyseer resultaten - welke topics ranken competitors maar wij niet?
4. Schrijf samenvatting naar `briefs/keyword-gaps-YYYY-MM-DD.md`

### 📊 Competitor Analyse
```
Analyze competitor content for [URL or topic]
```
Wat je doet:
1. Run `python scripts/scraper.py --url <competitor_url>`
2. Extraheer: word count, headings structuur, semantische keywords, interne links
3. Schrijf analyse naar `briefs/competitor-[naam]-YYYY-MM-DD.md`

### ✍️ Content Genereren
```
Write an article about [topic]
```
Wat je doet:
1. Lees `brand.md` voor voice guidelines
2. Voer eerst competitor analyse uit op top-3 rangerende pagina's
3. Schrijf SEO-geoptimaliseerd artikel gebaseerd op brand voice
4. Include: title, meta description, slug, H1/H2 structuur, FAQ sectie
5. Sla op als `content/[slug].md`

Output format:
```
---
title: [Title]
meta_description: [150 chars]
slug: [url-slug]
target_keyword: [primary keyword]
secondary_keywords: [lijst]
word_count: [number]
---

[artikel content]
```

### 📈 Rankings Tracken
```
Track rankings for all keywords
```
Wat je doet:
1. Run `python scripts/rank_tracker.py`
2. Vergelijk met vorige week (`rankings/` directory)
3. Schrijf rapport naar `rankings/report-YYYY-MM-DD.md` met:
   - Gestegen keywords (groen)
   - Gedaalde keywords (rood)
   - Nieuwe rankings
   - Top 10 keywords per positie

### 🎯 Volledig SEO Audit
```
Run full SEO audit
```
Voert alles uit: keyword gaps → competitor analyse → ranking report → aanbevelingen

## Backlink & Citation Commands

/seo backlinks <site>         - Vind backlink kansen voor site
/seo outreach <site> <target> - Genereer outreach content
/seo citations <site>         - Vind lokale directory kansen
/seo pipeline <site>          - Volledige pipeline: keywords → content → backlinks

### 🔗 Backlink Kansen Vinden
```
Find backlink opportunities for boomgaard
```
Wat je doet:
1. Lees `config.json` voor domain + niche
2. Run `python scripts/backlink_finder.py --site <domain> --niche "<niche>" --limit 20`
3. Analyseer output JSON - welke kansen zijn het meest waardevol?
4. Sla resultaten op naar `briefs/backlinks-YYYY-MM-DD.json`

### ✍️ Outreach Content Genereren
```
Generate outreach for boomgaard targeting vastgoedpro.nl
```
Wat je doet:
1. Run `python scripts/outreach_generator.py --site <site> --target-url <url> --type guest-post`
2. Output bevat: gastblog artikel + outreach email
3. Opgeslagen in `sites/<site>/briefs/outreach-<domain>-YYYY-MM-DD.md`

### 📍 Lokale Citations Bouwen
```
Find citation opportunities for boomgaard in Uithoorn
```
Wat je doet:
1. Run `python scripts/citation_builder.py --site boomgaard --city Uithoorn`
2. Output: lijst directories + NAP data template + actieplan
3. Opgeslagen in `briefs/citations-<stad>-YYYY-MM-DD.md`

### 🚀 Volledige SEO Pipeline
```
Run full SEO pipeline for boomgaard
```
Voert alles uit in volgorde:
1. Keyword gaps analyse
2. Content genereren voor top-3 kansen
3. Backlink kansen vinden
4. Citation lijst genereren
5. Samenvatting rapport schrijven

---

## Workflow Tips
- Begin altijd met `config.json` controleren
- Brand voice is heilig - altijd `brand.md` lezen voor content
- Rankings bijhouden: run weekly tracker elke maandag
- Content brief schrijven vóór het artikel

---

## Multi-site configuratie

Sites beschikbaar in `sites/` directory. Specificeer welke site bij commando's:
- `Run keyword gap analysis for gardano`
- `Write article for revive-woman about [topic]`
- `Track rankings for auto-boomgaard`
- `Analyze competitor for robin-bril`
- Zonder specificatie = gebruik hoofd config.json (Boomgaard&Munnik)

### Beschikbare sites

| Site | Directory | Domein | Niche |
|------|-----------|--------|-------|
| Boomgaard&Munnik | *(root)* | boomgaardfinancieel.nl | Zakelijk vastgoed financiering |
| Auto Boomgaard | sites/auto-boomgaard | autoboomgaard.nl | Premium occasion dealer Audi & Mercedes |
| Robin Bril AI | sites/robin-bril | robinbril.nl | AI agents / digitale medewerkers |
| REVIVE | sites/revive | revive-skin.nl | GHK-Cu skincare serum |
| Underground Royalty | sites/underground-royalty | rickpeper.nl | Kickboxen 1-op-1 training Leiden |
| Gardano | sites/gardano | christiaanwarner.nl | Brand & Creative Strategist |

### Per site beschikbare bestanden
- `config.json` - domain, competitors, keywords
- `brand.md` - brand voice, diensten, USPs
- `keyword-research.md` - uitgebreid keyword onderzoek + SEO rapport
- `content/` - gegenereerde artikelen
- `briefs/` - content briefs en analyses
- `rankings/` - ranking tracking

### Hoe een site te gebruiken
Wanneer je voor een specifieke site werkt:
1. Lees `sites/[naam]/config.json`
2. Lees `sites/[naam]/brand.md`
3. Raadpleeg `sites/[naam]/keyword-research.md` voor keyword context
4. Schrijf content naar `sites/[naam]/content/[slug].md`
