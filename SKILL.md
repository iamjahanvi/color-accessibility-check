---
name: color-accessibility-check
description: Use when building or reviewing UI code, tokens or screens for color accessibility: contrast ratios, non-text contrast, color-only meaning, and light/dark theme pairs.
---

# Color accessibility check

Target is WCAG 2.2 level AA. Apply while writing UI code and again when reviewing it.

## The three rules
1. **Text contrast.** Body text needs 4.5:1 against its background. Large text (24px+, or 18.66px+ bold) needs 3:1.
2. **UI parts.** Input borders, checkbox and toggle edges, icons that carry meaning, focus rings and selected states need 3:1 against what they sit on.
3. **Never color alone.** Any meaning carried by color (error, success, status, chart series, selected) also needs a second cue: icon, text label, pattern or position.

AAA (7:1 text) is a stretch goal, not the default. Disabled controls and pure decoration are exempt, but do not use that to hide real content.

## Workflow
1. List every foreground/background pair in the change: text on page, text on card, text on button, borders, icons, focus ring, placeholder, helper text, links.
2. Compute the ratio for each pair with a script, never by eye. Use relative luminance: channel = c/255; c<=0.03928 ? c/12.92 : ((c+0.055)/1.055)^2.4; L = 0.2126R + 0.7152G + 0.0722B; ratio = (Llight+0.05)/(Ldark+0.05). Round down, never up (4.499 fails 4.5).
3. Check pairs on their real surface. Text on a tinted chip is measured against the chip, not the page. Text over images or gradients is measured at the worst spot.
4. Fix by moving to a darker or lighter step of the same hue first, so the palette keeps its character. Change the hue only if no step passes.
5. Run the grayscale test: render the screen in grayscale (or a CSS grayscale(1) filter). Anything that disappears or becomes ambiguous breaks rule 3.
6. Report a table: pair, foreground, background, ratio, required, pass or fail, proposed fix.

## Tokens and themes
- Check contrast on semantic tokens (text.primary on surface.default), not raw palette values, so the fix lands once.
- Check every theme. Light and dark are separate pairs and each must pass on its own. Do not assume dark passes because light does.
- Do not auto-invert colors for dark mode. Re-pick each role: avoid pure black pages with pure white text, desaturate brand colors, replace shadows with surface elevation.
- Check states too: hover, pressed, focus, selected, error, disabled.
- Focus must be visible. Never remove outlines without a replacement that passes 3:1.

## Review checklist
- [ ] Every text pair at 4.5:1 (3:1 large)
- [ ] Borders, icons, focus rings at 3:1
- [ ] Status and errors have an icon or text, not only color
- [ ] Charts and legends separable without hue
- [ ] Light and dark both pass
- [ ] Grayscale render still readable

## Notes
- Ratios from screenshots are approximate; say so and prefer source values.
- Automated checks catch contrast only. Say plainly that meaning, focus order and screen reader behavior still need manual checks.
