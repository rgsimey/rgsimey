# rgsimey.scot — redesign prototype

Files
-----

```
rgsimey-prototype/
├── index.html        ← homepage
├── styles.css        ← main stylesheet (sections numbered, easy to find)
├── arran-map.css     ← map animation styles only
├── arran-map.svg     ← editable map (open in Affinity Designer)
├── images/           ← drop your existing images folder in here
│   ├── logo.png
│   ├── about-glenashdale.jpg
│   └── thumbs/
│       ├── thumb-books.jpg
│       ├── thumb-maps.jpg
│       ├── thumb-print.jpg
│       ├── thumb-branding.jpg
│       ├── thumb-logos.jpg
│       └── thumb-websites.jpg
└── README.md
```

Setup
-----

1. Copy your existing `images/` folder from rgsimey.scot into this
   directory. The HTML loads images by relative path.
2. Drop the Glenashdale childhood photo in as `images/about-glenashdale.jpg`
   when ready. If absent, the about section still works, just without the image.
3. Open `index.html` in a browser to view.

No build step, no framework. Upload everything to your web host's root
to go live.

The map
-------

The map uses your own outline (the one uploaded), at viewBox 260×320.
It contains:

- The stylistic wash shape you drew (preserved as-is)
- Main coastline + a slightly-offset sketch overlay (looks hand-drawn)
- Holy Isle
- Pladda
- Two raven glyphs from your original file

Animation sequence (when scrolled into view):

1. **0.2s** — Wash fades in underneath
2. **0.4s** — Coastline begins drawing (3.6s)
3. **0.7s** — Sketch overlay begins (3.8s, slightly offset second pass)
4. **2.6s** — Holy Isle pops in
5. **3.1s** — Pladda pops in
6. **3.5s** — First raven fades in
7. **4.1s** — Second raven fades in

Total sequence around 5.5 seconds. Plays once when the section
scrolls into view. To disable entirely, remove the `<script>` tag at
the bottom of `index.html` — the map will appear in its finished state.

Editing the animation
---------------------

All timing lives in `arran-map.css` as CSS variables at the top:

```css
--duration-coastline: 3.6s;   /* how long the coastline draws */
--duration-sketch: 3.8s;
--duration-wash: 2.2s;
--duration-raven: 1.4s;

--delay-wash: 0.2s;            /* when each element starts */
--delay-coastline: 0.4s;
--delay-sketch: 0.7s;
--delay-holy-isle: 2.6s;
--delay-pladda: 3.1s;
--delay-raven-1: 3.5s;
--delay-raven-2: 4.1s;

--coastline-weight: 2.2;       /* stroke weights */
--sketch-weight: 0.8;
--island-weight: 1.6;
```

Change a number, reload, see what happens.

Editing the map artwork
-----------------------

Open `arran-map.svg` in Affinity Designer. Edit any path. Save.
Then copy the path data back into `index.html` (find the inline
`<svg id="arranMap">` block).

The class names must stay for the animation to work:
- `class="arran-wash"`
- `class="arran-outline"`
- `class="arran-sketch"`
- `class="holy-isle-outline"`
- `class="pladda-outline"`
- `class="raven raven-1"` and `class="raven raven-2"`

Colours and typography
----------------------

In `styles.css`, the `:root` variables at the top:

```css
--paper: #f5f1ea;       /* page background */
--ink: #1a1a1a;         /* text + rules */
--rule: #1a1a1a;        /* thick broadsheet rules */
--rule-soft: #b8b0a0;   /* hairline rules */
--accent: #8b3a2e;      /* warm broadsheet red */

--font-display: 'Playfair Display', Georgia, serif;
--font-body: 'Fraunces', Georgia, serif;
--font-meta: 'Inter', sans-serif;
```

What's still to do
------------------

- Add the childhood photograph at `images/about-glenashdale.jpg`
- Build the inner project pages (books.html, maps.html, etc) — your
  existing pages can be restyled with these same stylesheets
- Photograph the publications properly (NatureScot handbook, Horizon
  Guides series, Interiors of Arran, Recipe Book, Geopark leaflet,
  Wildlife Code) and use those images on the project pages
- Decide whether you want first- or third-person on the lineage
  sentence (currently third)

Notes
-----

- Mobile-responsive at 800px breakpoint
- Respects `prefers-reduced-motion` (the map appears static for users
  who've requested less animation)
- Borders: 6px top/bottom on the masthead and footer, 3px between
  sections — adjust in `styles.css` if too heavy
