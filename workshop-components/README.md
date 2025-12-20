# Multiple Choice Quiz Component

A multiple-choice quiz component extracted from the Mathe-Advent calendar for use in Quarto-based workshops.

## Files

| File | Description |
|------|-------------|
| `multiple-choice.scss` | SCSS styling with customizable color variables |
| `multiple-choice.html` | JavaScript for quiz functionality |
| `test.qmd` | Test page with example questions |

## Quick Start

1. Add to your document's YAML header:
   ```yaml
   format:
     html:
       include-after-body: multiple-choice.html
       theme: [default, multiple-choice.scss]
   ```

   Note: SCSS must go in `theme:`, not `css:` — Quarto only compiles SCSS via the theme system.

2. Create questions using fenced div syntax (see below).

3. Preview with `quarto preview test.qmd` to test all features.

## Question Structure

```markdown
::: {.puzzle-box}
**Question:** What is 2 + 2?

<div class="quiz-options">
  <button class="quiz-option" data-correct="false">3</button>
  <button class="quiz-option" data-correct="true">4</button>
  <button class="quiz-option" data-correct="false">5</button>
</div>

<div class="quiz-actions">
  <p class="quiz-feedback"></p>
  <button class="quiz-submit" disabled>Submit</button>
</div>
:::
```

### Required Attributes

| Attribute | Element | Description |
|-----------|---------|-------------|
| `data-correct="true"` | `.quiz-option` | Marks the correct answer |
| `data-correct="false"` | `.quiz-option` | Marks incorrect options |
| `disabled` | `.quiz-submit` | Button starts disabled until selection |

### Optional Attributes

| Attribute | Element | Description |
|-----------|---------|-------------|
| `data-explanation="..."` | Correct `.quiz-option` | Shows explanation after correct answer |
| `data-penalty="5"` | `.quiz-submit` | Custom penalty time in seconds (default: 10) |
| `data-shuffle="false"` | `.quiz-options` | Disable option randomization |

## Features

### Accessibility
- **ARIA labels** — Screen reader support with `role="group"` and `aria-live` announcements
- **Keyboard navigation** — Arrow keys to navigate, Enter/Space to select
- **Visible focus indicators** — Clear outline on focused elements
- **Non-color state indicators** — Checkmarks and X marks for colorblind users

### User Experience
- **Randomized option order** — Shuffled on page load (can be disabled)
- **Attempt counter** — Shows "Attempt 2" etc. after wrong answers
- **Configurable penalty timer** — Adjustable wait time after wrong answers
- **Explanation support** — Optional explanation shown after correct answer
- **MathJax support** — Math notation renders correctly in options and explanations

### Mobile
- **Touch-friendly sizing** — Larger buttons and spacing on mobile
- **Full-width submit button** — Easier to tap on small screens

## Examples

### With Explanation

```markdown
::: {.puzzle-box}
**Question:** What is $2^{10}$?

<div class="quiz-options">
  <button class="quiz-option" data-correct="false">512</button>
  <button class="quiz-option" data-correct="true"
          data-explanation="2&lt;sup&gt;10&lt;/sup&gt; = 1024 because 32 × 32 = 1024">1024</button>
  <button class="quiz-option" data-correct="false">2048</button>
</div>

<div class="quiz-actions">
  <p class="quiz-feedback"></p>
  <button class="quiz-submit" disabled>Submit</button>
</div>
:::
```

**Note:** MathJax does not work in explanations. Use plain text or HTML (e.g., `&lt;sup&gt;` for superscripts).

### With Custom Penalty Time

```markdown
<button class="quiz-submit" data-penalty="5" disabled>Submit</button>
```

### With Shuffle Disabled

```markdown
<div class="quiz-options" data-shuffle="false">
  <!-- Options stay in authored order -->
</div>
```

## Customization

### Colors (in SCSS)

```scss
$color-primary: #a00028;        // Main accent (burgundy)
$color-correct: #a7c7c6;        // Success background (teal)
$color-correct-border: #537e8f; // Success border
$color-wrong: #ebadad;          // Error background
$color-wrong-border: #db6b6b;   // Error border
```

### Feedback Messages

Edit in `multiple-choice.html`:
- Line 101: Success message (`"Correct!"`)
- Line 143: Error message template

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| Tab | Move focus to next element |
| Arrow Up/Down | Navigate between options |
| Arrow Left/Right | Navigate between options |
| Enter / Space | Select focused option |

## Multiple Questions

Add multiple `::: {.puzzle-box}` blocks. Each operates independently with its own state and attempt counter.
