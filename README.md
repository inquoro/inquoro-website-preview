# Inquoro Website Preview

Static HTML/Tailwind mockup of the Inquoro marketing website for team review. Built to make it easy to translate into the existing MakerKit (Next.js) codebase.

**Live preview:** https://inquoro.github.io/inquoro-website-preview/

## For Adam: Translation Guide

### How This Maps to MakerKit

This is a single `index.html` using **Tailwind CSS via CDN** — the same utility classes the MakerKit template already uses. Each `<section>` maps 1:1 to a page section and is clearly commented:

| HTML Section | Comment Tag | MakerKit Target |
|---|---|---|
| Navigation | `<!-- NAVIGATION -->` | Replace existing nav component |
| Hero | `<!-- SECTION 1: HERO -->` | Replace existing hero |
| Mission | `<!-- SECTION 2: THE MISSION -->` | New section (after hero) |
| The Beamline | `<!-- SECTION 3: THE BEAMLINE -->` | Replaces "À La Carte Services" intro |
| Population Sources | `<!-- SECTION 4: POPULATION SOURCES -->` | Replaces "Research Panel" + "Survey Recruitment" |
| Measurement | `<!-- SECTION 5: MEASUREMENT -->` | New section (Primary Signal + Signal Scan + Resonance Detector) |
| The Difference | `<!-- SECTION 6: THE DIFFERENCE -->` | Replaces "Why Choose Inquoro?" cards |
| Who We Work With | `<!-- SECTION 7: WHO WE WORK WITH -->` | New section |
| Inference Engine | `<!-- SECTION 8: INFERENCE ENGINE -->` | New section |
| Contact | `<!-- SECTION 9: CONTACT -->` | Update existing contact form |

### Brand Color Tokens

Update `tailwind.config.js` in the MakerKit project:

```js
// Replace the existing primary/accent colors with:
colors: {
  navy:    '#31344e',  // Primary backgrounds, headings, dark sections
  brown:   '#64463c',  // Subtle accent — borders, hover darkening, footer
  amber:   '#a96e38',  // CTA buttons, links, highlights, key callouts
  slate:   '#586582',  // Subheadings, secondary buttons, icon fills
  silver:  '#a8aebd',  // Dividers, muted text, card borders, placeholders
}
```

The MakerKit template uses CSS custom properties for `--primary` etc. Map them:
- `--primary` → `#a96e38` (amber)
- `--primary-foreground` → `#ffffff`
- Dark sections use `#31344e` as background

### Typography

```html
<!-- Google Fonts (add to _document or layout head) -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Jost:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

```js
// tailwind.config.js
fontFamily: {
  heading: ['Jost', 'Futura', 'system-ui', 'sans-serif'],  // Section headings
  body: ['Inter', 'system-ui', 'sans-serif'],               // Body text (already in MakerKit)
}
```

**Logo font is ITC Bauhaus** — Jost is chosen as the heading font because it shares the geometric DNA (circular forms, even stroke weight) without competing with the logo.

### Logo Files

All in `assets/images/`:
- `Inquoro_logo_text-*.png` — Logo + "Inquoro" text (for nav, footer)
- `inquoro_logo-*.png` — Icon only (for favicon, hero, loading)
- `web/` — Optimized versions for web use

Replace the inline SVG `<text>` element in MakerKit's nav/footer with actual `<img>` tags using these files.

### What's Static vs. Interactive

- **Contact form** — Currently just HTML. Wire it up to your existing form handler.
- **Navigation** — Mobile menu toggle is vanilla JS. Replace with your React menu component.
- **Auth (Sign In/Sign Up)** — Not included. Keep the existing MakerKit auth flow.
- **Dashboard/SaaS features** — Not included. This is marketing pages only.

### Section Rhythm (Dark/Light)

The alternating background pattern creates visual rhythm:
```
Hero        → dark  (#31344e gradient)
Mission     → light (white)
Beamline    → light (gray-50)
Sources     → light (white)
Measurement → dark  (#31344e gradient)
Difference  → light (white)
Who We Work → light (gray-50)
Inference   → dark  (#31344e gradient)
Contact     → light (white)
Footer      → dark  (#31344e solid)
```

### Copy Source

All website copy lives in the Google Doc:
**[Inquoro Website Copy — Wren Draft](https://docs.google.com/document/d/1zUwi5AUZ-lJvDgp-8NujPoAGdS2jbslrgtoGD_NsK2w/edit)**

The doc includes section-by-section design notes in `< >` brackets.

## Development

No build step required. Just open `index.html` in a browser:

```bash
open index.html
# or
python3 -m http.server 8080  # then visit localhost:8080
```

## File Structure

```
├── index.html              # The full site mockup
├── README.md               # This file
└── assets/
    └── images/
        ├── web/            # Optimized web versions
        │   ├── logo-text-alpha.png
        │   ├── logo-text-white.png
        │   ├── logo-text-alpha-lg.png
        │   ├── logo-icon-alpha.png
        │   └── logo-icon-alpha-lg.png
        ├── Inquoro_logo_text-*.png   # Full-res originals
        └── inquoro_logo-*.png        # Full-res originals
```
