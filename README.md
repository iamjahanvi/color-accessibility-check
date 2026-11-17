# color-accessibility-check

A skill for Claude that checks UI color for accessibility: contrast ratios, non-text contrast, color-only meaning and light/dark theme pairs. Made for the Molades Visual Anatomy course, Session 04 "Colors in Practice".

## Use it in Claude Code
Copy this folder into your project:

```
.claude/skills/color-accessibility-check/SKILL.md
```

Then ask Claude to check a screen, a component or your color tokens for accessibility.

## Use it in Claude (web or desktop)
Upload `SKILL.md` as a custom skill in your Claude settings.

## What it checks
1. Text needs 4.5:1 (3:1 for large text)
2. UI parts (borders, icons, focus rings) need 3:1
3. Never use color alone to carry meaning

Light and dark themes are checked separately. WCAG 2.2, level AA.
