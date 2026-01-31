# Lazy Articles

A Claude Code skill that automatically tracks your development process and generates engaging articles/case studies about your projects.

## What it does

- **Tracks** your development journey: ideas, struggles, breakthroughs, solutions
- **Generates** articles using storytelling techniques
- **Supports** multiple languages (Russian/English) and tones of voice
- **Trains** on your writing style for personalized output

## Quick Start

1. Add this project's `CLAUDE.md` to your project
2. Run `/article start` to begin tracking
3. Build your project as usual
4. Run `/article generate` when ready to create your article

## Commands

| Command | Description |
|---------|-------------|
| `/article start` | Begin tracking development |
| `/article pause` | Pause tracking (for sensitive work) |
| `/article resume` | Resume tracking |
| `/article generate` | Generate article from tracked events |
| `/article train` | Train custom TOV on your texts |
| `/article settings` | View/modify configuration |

## TOV Presets

- **Technical** - Documentation-style, precise, reproducible
- **Blog** - Conversational, personal, relatable
- **Corporate** - Professional case study, business-focused
- **Viral** - Hook-heavy, emotional, shareable
- **Custom** - Train on your own texts

## File Structure

```
.lazy-articles/
├── tracking.json    # Event log
├── config.json      # Settings
├── drafts/          # Generated articles
└── training/        # Your sample texts for TOV training
```

## Coming Soon

- Flammelis Style TOV preset
- More storytelling templates
- Export to specific platforms (Medium, Habr, Dev.to)
