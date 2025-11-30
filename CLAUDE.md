# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Quarto website implementing a German mathematics advent calendar themed around "The Grinch" for 2025. Students solve interactive math puzzles to progress through a narrative about defeating GrinchTech's algorithms.

## Build Commands

```bash
# Render the entire site
quarto render

# Preview with live reload
quarto preview

# Render a single day
quarto render days/day01.qmd
```

## Architecture

### Content Structure
- `index.qmd` - Main landing page with advent calendar grid (24 doors)
- `days/dayXX.qmd` - Individual daily challenges (day01-day24)
- `404.qmd` - Error page

### Quiz System
The interactive quiz system uses vanilla JavaScript (in `calendar.html`) with two question types:

1. **Multiple Choice** - Buttons with `class="quiz-option"` and `data-correct="true/false"`
2. **Text Input** - Input field with `class="quiz-input"`, submit button has `data-answer="correct_answer"`

Quiz structure in `.qmd` files:
```html
::: {.scenario-block}
::: {.puzzle-box}
<!-- quiz-option buttons or quiz-input field -->
<div class="quiz-actions">
  <p class="quiz-feedback"></p>
  <button class="quiz-submit" disabled>Submit</button>
</div>
:::
::: {.revealed-text}
<!-- Content shown after solving all puzzle-boxes in scenario -->
:::
:::
```

### Styling
- `_brand.yml` - Color palette and typography (Gelasio, Reddit Sans, Google Sans Code fonts)
- `styles.scss` - SCSS variables and utility classes
- `advent.css` - Calendar door grid styling with date-based locking
- `quiz.css` - Quiz component styling (buttons, inputs, feedback states)

### Door Locking Logic
`calendar.html` contains JavaScript that:
- Locks future days (doors with `data-day` > current date in December 2025)
- Highlights today's door with pulsing animation
- `debugMode = true` unlocks all doors for testing

## Conventions

- Math rendered with MathJax (configured in `_quarto.yml`)
- Each day's QMD must include `include-after-body: ../calendar.html` and the CSS files
- Colors reference brand palette variables (e.g., `$brand-twoDark`, `$brand-threeDark`)
