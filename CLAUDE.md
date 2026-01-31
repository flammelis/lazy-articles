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
   - TOV style: technical, blog, corporate, viral, flammelis, or custom (if trained)
   - Technical depth: beginner-friendly or expert-level
2. **Ask for personal input:**
   - "What emotions did you feel during key moments? Any frustrations, excitement, relief?"
   - "Any personal details or context you want included that I might have missed?"
   - "Any specific moments you want highlighted or downplayed?"
3. Generate draft using storytelling techniques
4. Save to `.lazy-articles/drafts/` with timestamp
5. Present draft for review
6. Ask if user wants adjustments before final version

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

## On Session Start (Auto-Resume)

**IMPORTANT**: At the start of EVERY new Claude Code session in this project:

1. Check if `.lazy-articles/config.json` exists
2. If `trackingActive: true`, automatically resume tracking
3. Silently continue logging events to `tracking.json`
4. No need for user to run `/article resume` - it happens automatically

This ensures tracking persists across multiple Claude Code sessions.

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

### Storytelling Structures
Choose the best fit for the project:

1. **Three-Act Structure** - Set up → Confrontation → Resolution
2. **Freytag's Pyramid** - Exposition → Rising action → Climax → Falling action → Dénouement
3. **Hero's Journey** - Protagonist goes on adventure → Wins victory → Returns transformed
4. **In Medias Res** - Start in the middle of action, then fill in context
5. **Fichtean Curve** - Series of crises immediately following introduction
6. **Story Circle** - Character arc driven by desire and change
7. **Problem-Solution Loop** - Multiple mini-arcs of challenge → attempt → resolution
8. **Before/After Contrast** - Paint the pain, then the relief
9. **Behind the Scenes** - Raw, authentic "here's what really happened"

### Narrative Devices
Enhance the story with:

- **Flashback/Flashforward** - Alter time sequence for context or foreshadowing
- **Foreshadowing** - Drop subtle hints about what's coming
- **Frame Story** - Story within a story (narrator telling about another experience)
- **Show, Don't Tell** - Use descriptive language and actions over exposition
- **Stream of Consciousness** - Represent unfiltered, continuous thought process
- **Perspective Shifts** - Move between first/second/third person viewpoints
- **Pattern Interrupts** - Break expectations to grab attention

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

**Flammelis Style** (Russian viral tech storytelling)
- First-person confessional, "talking to a friend" voice
- Self-deprecating humor, ironic but not bitter
- Creative chapter names and character introductions with emojis
- Wordplay/puns in titles, anti-success framing ("Как НЕ стать...")
- Foreshadowing device ("Спойлер: легче не было")
- Russian internet slang (рыночек, факап, хайп, юзкейс, штош)
- Pop culture references and creative metaphors
- Behind-the-scenes authenticity, show the messy middle
- P.S. at the end with numbers/insights
- Concrete results and honest emotions throughout

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
