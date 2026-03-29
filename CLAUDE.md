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

## Workflow Tips
- Begin altijd met `config.json` controleren
- Brand voice is heilig - altijd `brand.md` lezen voor content
- Rankings bijhouden: run weekly tracker elke maandag
- Content brief schrijven vóór het artikel
