# DESIGN.md — Site Rebuild Brief

> This file is the north-star context for rebuilding my personal site.
> Read it fully before doing anything. Re-read it at the start of any future session.
> I am the owner (Chris). You are Claude Code working in this repo on my machine.

---

## 0. What this is

A rebuild of my personal site (currently a hand-rolled `index.html` + `content.js`
on GitHub Pages at `christhomas96.github.io`) into a modern, atmospheric, weird
personal site organised as a **memory palace** — a house of rooms you move through,
where each room is a different mode of thought.

The old site is flat: all my posts (tech, magick, geopolitics, personal, PM work)
sit in one feed, which makes an eclectic range read as incoherent. The memory-palace
structure fixes this: each kind of thinking gets its own **room**, so range becomes
architecture instead of noise.

This is a personal weekend project. Bias toward shipping something real and good-looking
over perfection. Atmosphere and structure carry the weirdness — NOT piles of effects.

---

## 1. Concept: the memory palace (method of loci)

The method of loci / "memory palace": ideas placed in rooms of an imagined building,
recalled by walking through it. Renaissance Hermeticists (Camillo's Theatre of Memory,
Giordano Bruno) extended it into the *art of memory*, where rooms held archetypes and
cosmic correspondences. That's the spirit of this site.

**Critical design constraint — atmosphere, NOT simulation:**
- This is NOT a literal explorable 3D house. NOT a top-down 2D floor plan / blueprint.
- It IS a dark, deep space where rooms exist as **thresholds** you move toward and pass through.
- The "house" feeling comes from: depth, parallax, soft light, slow motion, and
  page-to-page **view transitions** that morph one room into the next like passing
  through a doorway.
- Reading any actual post must always be one tap/click away. Never bury the writing
  behind a game.
- Must work and feel good on **mobile** (I'm often on phone). Fast, static, accessible.

---

## 2. The rooms

Six rooms. Each is a section. Adding a room later must be cheap.

| Room | Slug | Holds | Mood |
|---|---|---|---|
| **The Threshold** | `/` | Landing/entry. Name low and quiet, doorways/lights leading inward. NOT a homepage feed. | Dim, anticipatory |
| **The Study** | `/study` | Writing — essays, half-formed thoughts, eclectic posts. The main blog room. | Manuscript, warm |
| **The Observatory** | `/observatory` | Astrology, Hermetic philosophy, cosmology, my chart, dasha notes, sky-and-symbol. | Cosmic; the one place the cold counter-tone appears |
| **The Workshop** | `/workshop` | The maker side: PM work, things I build, tech writing, this site itself. Resume/portfolio signal WITHOUT being a LinkedIn clone. | Functional, mono |
| **The Long Room** | `/long-room` | Shadow-work, Jungian, psyche-and-meaning material. Deeper in the house, more personal. Can be collapsed into Study later if it feels like too much. | Darker, quieter |
| **Now** | `/now` | Always-current: where I am, what I'm training, riding, reading. The page I update most. | Small, lit, present |

Posts get assigned to a room. A post can default to The Study if unroomed.

---

## 3. Aesthetic spine

Keep restraint. The weird comes from atmosphere + structure, not from effect-piling.
Avoid looking like a Geocities occult page.

**Palette**
- Base: near-black, deep and warm (not pure #000 — slightly warm charcoal).
- Primary accent: warm gold / candle-amber. Does all the emotional work. Used for
  light sources, active states, key type.
- Cold counter-tone: a pale astral blue. Used ONCE, in The Observatory only. Nowhere else.
- Generous negative space (negative *dark* space here).

**Typography**
- Body: a serif (manuscript / memory-palace feel). Readable, slightly classical.
- Labels / metadata / nav / Workshop: a monospace (my systems side).
- Strong contrast between the two is intentional.

**Motion**
- Slow. Nothing snappy or "productY." No bouncy micro-interactions.
- Page transitions feel like moving between rooms, not loading pages.
- Subtle parallax / drift / soft light. Respect `prefers-reduced-motion` — provide a
  calm static fallback.

---

## 4. Tech stack

- **Astro** (static site generator). Posts as Markdown files in content collections.
- **Astro View Transitions** for the room-to-room threshold feel.
- Plain CSS or lightweight CSS (no heavy framework). Tailwind only if you think it helps;
  otherwise vanilla CSS with custom properties for the palette is fine and preferred.
- Hosted on **GitHub Pages**, same repo (`christhomas96.github.io`). Free.
- Build/deploy via GitHub Actions (Astro's official GH Pages workflow).
- A custom domain may be pointed later via one DNS record — leave room for a `CNAME` file
  but don't block on it. Site must work fine on the `.github.io` URL.

---

## 5. Content model

Use an Astro content collection `posts` with this frontmatter schema:

```
---
title: string
date: date
room: 'study' | 'observatory' | 'workshop' | 'long-room'   # default 'study'
tags: string[]
excerpt: string
draft: boolean   # default false
---
```

Plus standalone pages for The Threshold (`/`), Now (`/now`), and an About surfaced
somewhere unobtrusive (e.g. within The Threshold or its own quiet page).

---

## 6. MIGRATION — port existing posts (do this carefully)

The old content lives in `content.js` in this repo (currently committed). It contains:
- `ABOUT` object
- `NOW` object (location, sections)
- `POSTS` array — each post is an object: `{ id, date, tag: [], title, excerpt, body }`
  where `body` is an HTML string (`<p>...</p>`, `<em>`, etc.).

Known existing posts (verify against the actual file — there may be more, including a
newer essay on retrospective meaning-making):
- `on-magick` — ritual as psychology ("psychology with better aesthetics") → room: long-room or observatory
- `on-relocation` — "On moving to a city you already half-live in" (Feb 2026) → room: study (tags: personal)
- `ai-product-management` — "What AI actually changes about being a PM" (Jan 2026) → room: workshop (tags: tech, product)

**Migration steps:**
1. Read `content.js`. Enumerate every object in `POSTS` — do not rely on the list above,
   use whatever is actually in the file.
2. For each post, create `src/content/posts/<id>.md`:
   - `title`, `date`, `excerpt`, `tags` (from `tag`) → frontmatter.
   - Assign a `room` using judgment from tags/content (ask me if genuinely unsure;
     otherwise default to `study`).
   - Convert the `body` HTML string to Markdown (`<p>`→paragraphs, `<em>`→`*italic*`, etc.).
   - Preserve the writing exactly — do not rewrite my prose.
3. Port `ABOUT` into the About surface and `NOW` into the `/now` page.
4. Keep the old `index.html` and `content.js` in the repo (or move to an `/_old` folder)
   until I confirm the new site is good — do NOT delete them yet.
5. Show me a diff/summary of what was migrated before moving on.

---

## 7. Build order (do these in sequence, pause for my review between phases)

1. **Scaffold** — init Astro in this repo without nuking existing files; set up the
   content collection, base layout, palette as CSS custom properties, the two fonts.
   Get a blank dark base rendering locally (`npm run dev`).
2. **Migrate** — section 6. One pass, then show me the result.
3. **The Study** — first real room: list of posts + a single-post template. Get reading
   working end-to-end with migrated content.
4. **The Threshold** — the landing/entry with doorways to rooms. View transitions between
   Threshold ↔ Study working.
5. **Remaining rooms** — Observatory, Workshop, Long Room, Now. Each themed per section 2/3.
6. **Atmosphere pass** — parallax, soft light, drift, reduced-motion fallback. Mobile check.
7. **Deploy** — GitHub Actions → GitHub Pages. Confirm live on `.github.io`.

After each phase: brief summary of what changed + what to look at. Don't run ahead.

---

## 8. Working notes for you (Claude Code)

- Don't copy-paste-dump huge files into chat; you have direct file access — just edit.
- Commit in logical chunks with clear messages. Don't force-push or rewrite history.
- Ask before any destructive action (deleting old files, overwriting the live entrypoint).
- Mobile-first and accessible: semantic HTML, keyboard-navigable rooms, alt text,
  `prefers-reduced-motion`.
- Keep it fast: static output, minimal JS, no heavy libraries for the atmosphere —
  CSS and the native View Transitions API first.
