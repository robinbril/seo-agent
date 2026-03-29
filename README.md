# SEO Agent

Claude Code SEO agent die Ahrefs vervangt. Geen extra API keys nodig - gebruikt Brave Search.

## Setup

1. Edit `config.json` - vul je domain, competitors en target keywords in
2. Edit `brand.md` - beschrijf je brand voice en schrijfstijl  
3. Open Claude Code in deze directory: `claude` (of start Claude Code met deze folder)
4. Type een prompt en de agent doet de rest

## Prompts

```
Run keyword gap analysis against competitors
Analyze competitor content for https://competitor.com/article  
Write an article about [topic]
Track rankings for all keywords
Run full SEO audit
```

## Wekelijkse Cron

Rankings worden bijgehouden in `rankings/`. Stel een wekelijkse cron in:

```
python scripts/rank_tracker.py
```

## Environment

`BRAVE_API_KEY` moet beschikbaar zijn (staat al in OpenClaw config).
