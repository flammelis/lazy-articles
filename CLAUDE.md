# Lazy Articles Skill

A Claude Code skill that tracks your development process and generates engaging articles/case studies about your projects.

## Commands

### `/article start`
Begin tracking the development session.
- On first run: ask user what information should always be excluded (credentials, company names, personal data, etc.)
- Save exclusions to `.lazy-articles/config.json`
- Start logging events to `.lazy-articles/tracking.json`

### `/article pause`
Temporarily stop tracking. Use when working with sensitive data.
- Log pause event with timestamp
- Do not track any events until resumed

### `/article resume`
Resume tracking after pause.
- Log resume event with timestamp
- Continue normal tracking

### `/article generate`
Generate an article from tracked events.
1. Ask user for:
   - Language: Russian (RU) or English (EN)
   - TOV style: technical, blog, corporate, viral, or custom (if trained)
   - Technical depth: beginner-friendly or expert-level
2. Generate draft using storytelling techniques
3. Save to `.lazy-articles/drafts/` with timestamp
4. Present draft for review
5. Ask if user wants adjustments before final version

### `/article train`
Train a custom TOV on user's texts.
- User places their sample texts in `.lazy-articles/training/`
- Analyze texts for: tone, structure, hooks, transitions, vocabulary, emotional patterns
- Save extracted style profile to `.lazy-articles/config.json` under `customTOV`

### `/article settings`
View or modify current configuration.
- Show current settings (exclusions, default language, default TOV)
- Allow modifications

---

## Tracking Behavior

When tracking is active, continuously observe and log:

### What to Track
1. **Ideas & Goals** - Initial problem statement, what user wants to build
2. **Technical Decisions** - Architecture choices, tool selections, library picks
3. **Struggles & Attempts** - Failed approaches, errors encountered, debugging sessions
4. **Breakthrough Moments** - "Aha!" realizations, unexpected solutions, Claude suggestions that worked
5. **Technical Solutions** - How problems were actually solved (commands used, code patterns, ultrathink insights)
6. **Milestones** - Features completed, tests passing, deployments

### How to Log
Add events to `.lazy-articles/tracking.json` as array of objects:
```json
{
  "timestamp": "ISO-8601",
  "type": "idea|decision|struggle|breakthrough|solution|milestone",
  "summary": "Brief description",
  "details": "Full context, code snippets if relevant",
  "emotion": "frustrated|curious|excited|satisfied|neutral"
}
```

### What NOT to Track
- Anything matching exclusion patterns in config
- Events during pause mode
- Routine file reads without meaningful context
- Redundant repetitive actions

---

## Article Generation Guidelines

### Storytelling Techniques
Choose the best fit for the project:

1. **Hero's Journey** - Problem → Challenges → Mentor (Claude) → Transformation → Victory
2. **In Medias Res** - Start with the breakthrough, then flashback to how we got there
3. **Problem-Solution Loop** - Multiple mini-arcs of challenge → attempt → resolution
4. **Before/After Contrast** - Paint the pain, then the relief
5. **Behind the Scenes** - Raw, authentic "here's what really happened"

### TOV Presets

**Technical**
- Clear, precise language
- Step-by-step explanations
- Code examples with comments
- Focus on reproducibility

**Blog**
- Conversational tone
- Personal anecdotes
- Relatable analogies
- Light humor welcome

**Corporate**
- Professional case study format
- Business value emphasis
- Metrics and outcomes
- Credibility markers

**Viral**
- Strong hook in first line
- Emotional engagement
- Unexpected twists
- Shareable insights
- Pattern interrupts

### Language Rules
- If user selects Russian: Write article in Russian
- If user selects English: Write article in English
- ALWAYS keep in English regardless of article language:
  - Code snippets
  - Terminal commands
  - File paths
  - Technical terms that don't translate well
  - Tool/library names

### Technical Depth

**Beginner-friendly**
- Explain concepts before using them
- Avoid jargon or define it
- More context, simpler code examples
- "Why" before "how"

**Expert-level**
- Assume technical knowledge
- Focus on interesting/novel approaches
- Deeper implementation details
- Trade-off discussions

---

## File Structure

```
.lazy-articles/
├── tracking.json    # Event log (array of tracked events)
├── config.json      # Settings: exclusions, defaults, custom TOV
├── drafts/          # Generated articles (markdown files)
└── training/        # User's sample texts for TOV training
```

---

## Initial Setup

On first `/article start`, create config.json with:
```json
{
  "exclusions": [],
  "defaultLanguage": null,
  "defaultTOV": null,
  "defaultDepth": null,
  "customTOV": null,
  "trackingActive": false,
  "projectName": ""
}
```
