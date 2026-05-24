# Design DNA — Round 2 References

Reconnaissance for 3 new luxury-events mockups for Chris Sullivan (private events / galas / weddings / corporate). All notes captured from live DOM + visual analysis on the dates listed. Goal: extract reusable patterns, not literal copy. Translate "pop-artist merch" cues into "luxury entertainment company" cues.

---

## 1. justinbiebermusic.com — Hero Video Treatment

**Bela's call-out:** "How the video sits on the front page."

### Hero video player — exact mechanics
- **Implementation:** NOT a true inline `<video>` element. It is a **click-to-launch lightbox**. The "player" on the homepage is a `<figure class="article-figure">` whose background is set to a YouTube thumbnail (`img.youtube.com/vi/{id}/maxresdefault.jpg`) sized `background: cover`. A centered `<a class="play-button" data-fancybox href="https://www.youtube-nocookie.com/watch?v={id}">` with an SVG triangle play icon sits in an `.overlay` div above it.
- **Aspect ratio:** **16:9 exactly** (DOM measured 1.7777). Clean letterboxed rectangle.
- **Autoplay/muted/loop/controls:** None on the page itself — the page shows a still frame. Video only plays after click, inside a Fancybox modal (YouTube embed, so YT controls appear in the modal, not the homepage).
- **Position on page:** Center-column, below the tour section ("Sorry, no shows currently / RSVP"), above the newsletter form. Carousel with Previous / Next chevron buttons flanking the figure on either side — implying multiple videos rotate through the same slot.
- **Overlays on top of the still frame:**
  - Big centered circular play SVG (white, ~50px).
  - Video title burned into the thumbnail itself ("BAD HONEY" in white display type) — handled at the image level, not as HTML overlay.
- **Surrounding negative space:** Generous dusty-pink (`#F8B5C6`) margin on all four sides — the video does NOT bleed to viewport edges. It is a contained rectangle that floats inside the pink page, framed by lots of breathing room.
- **Above:** Tour-dates block (centered serif type + RSVP link).
- **Below:** Pink newsletter capture form (email + country select + opt-in checkboxes + submit).

### Full palette
| Hex | Role |
|---|---|
| `#F8B5C6` | Page background (signature dusty pink) |
| `#535353` | Body text (warm grey, not pure black) |
| `#222222` @ 50% | Soft black overlays |
| `#FFFFFF` | Card / form backgrounds, video play icon |
| `#CC0000` | Error / accent red (form validation) |
| `#7D7D7D` / `#808080` | Secondary greys |

### Typography
- **Display / H1 ("JUSTIN BIEBER"):** `Swag` (custom display serif) → fallback HelveticaNeue-Light. ~20px wordmark scale.
- **Body / forms:** `Playfair Display` (400, 700) and `Amiko` (400).
- **System fallbacks:** Roboto italic + Roboto regular variable axes loaded.
- Heavy editorial, almost fashion-magazine feel. All-caps everywhere.

### Nav structure
- **Top-left:** "JUSTIN BIEBER" wordmark (also serves as home link).
- **Top-right:** Social icons (IG, TikTok, FB, X) + single "SHOP" link. No mega-nav. Aubergine/dark plum header bar.
- **No secondary menu.** Whole site funnels into Shop + Social.

### Footer
- Single thin line of all-caps grey links on pink: `COPYRIGHT DEF JAM · PRIVACY POLICY · TERMS & CONDITIONS · DO NOT SELL MY PERSONAL INFORMATION · COOKIE CHOICES`. No columns, no socials in footer (they live in header).

---

## 2. chrisbrownworldstore.com — Hero Portrait & Palette

**Bela's call-out:** "Color palette and how the artist photo sits at the top of the page."

### Hero portrait — exact composition
- **Framing:** **Full-body, horizontal/cinematic.** Chris is reclining on his side on a shaggy cream rug, propped on one elbow — editorial album-cover pose, not a candid. Left third of the frame = typography & CTA, right two-thirds = the body.
- **Wardrobe:** Tan/camel monochrome suit + matching wide-brim fedora — color-matched to the entire page so the figure dissolves into the palette rather than pops off it.
- **Background treatment:** Dark chocolate gradient with a subtle vignette pulling focus to center. The entire hero is bathed in a unifying sepia/warm-brown wash — photo, type, and bg share one color temperature.
- **Overlay typography:** "CHRIS BROWN" eyebrow in spaced sans caps + giant ornate serif "BROWN" album wordmark + "3LP BLACK ICE GLITTER VINYL" subline + "PRE-ORDER NOW" pill CTA. A vinyl record peeks out from behind the album art on the far right edge — a deliberate diegetic prop.
- **Dimensions:** Desktop banner asset 2400×1000-ish (1280×533 rendered). Mobile served separately (873×1310 portrait crop) — they shoot/composite a vertical variant rather than letting CSS crop.
- **Position:** Full-bleed at the very top under a transparent header. No padding around the banner — edge to edge.
- **Below the hero:** Featured product (the vinyl) with gallery viewer, price ($54.98), quantity stepper, Add to Cart, Shop Pay installments link.

### Full palette
| Hex | Role |
|---|---|
| `#422112` | Primary deep chocolate (header bg, dark surfaces) |
| `#DBAE6F` | Camel / tan — primary text & accent color |
| `#F3F4EA` | Off-white cream (product surfaces, contrast panels) |
| `#000000` | Pure black (vinyl, deep shadow) |
| `#FFFFFF` | Reserved for high-contrast moments |
| `rgba(219,174,111,0.75)` | Body text — the camel softened |
| `rgba(66,33,18,0.85)` | Sticky header overlay |

The whole site lives in a **chocolate × camel × cream** triad. Monochromatic by design.

### Typography
- **Display script ("BROWN"):** `AT Arges` — ornate serif with decorative swashes.
- **Display sans / wordmarks:** `Futura Std Bold` (body default), `Jost` 700 & 800 (italic + roman) for headings.
- **Editorial sans:** `GTStandard-M` weights 450/500/600 for product copy.
- **UI fallback:** `InterVariable`.

### Nav structure
- **Top bar:** centered Chris Brown wordmark (camel on chocolate), search left, login + cart right.
- **Secondary horizontal menu** beneath: `COLLECTIONS · APPAREL · ACCESSORIES · MUSIC · TOUR · SALE` — all in camel uppercase, mega-dropdown on hover (buttons have `aria-expanded`).
- Sticky on scroll.

### Footer
- Multi-column on chocolate background, camel headings:
  - **STORES:** UK / EU regional links.
  - **LINKS:** Search, Returns, Contact, Terms, Privacy, Cookies, DNSMPI.
  - **SIGN UP** newsletter (email + Subscribe).
  - **Social row:** FB, IG, YT, X.
  - **Country/region picker:** "USD $ | United States" dropdown.
- Tiny baseline: CHRIS BROWN © + "MERCH TRAFFIC" platform credit.

---

## 3. legendary.com — Rotating Video Hero

**Bela's call-out:** "The rotating videos on the homepage."

### Video gallery — exact mechanics
- **Count:** **3 slides in rotation** (looped: Minecraft → Street Fighter → Dune: Part Three, then back). DOM duplicates each slide once for the infinite-loop trick (so 6 `<li>` total, 3 unique). 3 pagination dots confirm 3 logical slides.
- **Implementation:** Slick-style carousel (`<ul>` of `<li>` slides each holding a `<video>` + title `<h2>` + "DISCOVER MORE" anchor).
- **Video elements:** Native HTML5 `<video>`, sources are `.mp4` hosted on the WP uploads dir (e.g. `minecraft-website-cutdown.mp4`, `SF-website.mp4`). Dune slide carries **no video, just a still** — title + CTA only; mixed media is fine in the same carousel.
- **Dimensions:** Rendered 1120×625 (≈16:9, technically 1.79:1). Sits inside a centered max-width container — NOT full-bleed; there's a thin dark-navy gutter on either side.
- **Autoplay / muted / loop / controls:** All hero `<video>` elements are `muted=true`, `controls=false`. Interestingly `autoplay=false` and `loop=false` on the markup — the carousel script triggers `.play()` when a slide becomes active and advances on `ended`. So the video plays through once, then carousel moves to next slide (video-length-driven timing, not a fixed timer). **No audio ever.**
- **Transition style:** Horizontal slide (Slick default `slide`), with Previous/Next chevrons mid-height left & right and 3 dots centered below the hero. Smooth slide-in, not crossfade.
- **UI on top of the videos:**
  - Bottom-center: large title (`<h2>` like "A MINECRAFT MOVIE") in trumpsoftpro serif italic, plus a thin **outlined white "DISCOVER MORE" pill** CTA. Minimal — entire bottom area is reserved for one title + one CTA, nothing else.
  - Top: transparent header floats over the video (Legendary globe logo left, FILM/TV/COMICS/NERDIST/LATEST NEWS/ABOUT/SHOP center, socials right).
  - Sides: Prev/Next arrows.
  - No volume / scrubber / fullscreen UI — videos are atmospheric backdrops, not playable assets.
- **Mobile handling:** A separate `1080x1920` vertical Minecraft cutdown (`US_Minecraft_BeeAWDomestic_10s_1080x1920.mp4`) is in the DOM with `autoplay=true, loop=true, muted=true` — confirming a **mobile-specific portrait video swap** rather than CSS cropping a landscape file. Vertical mobile videos are short (10s) and DO loop unlike desktop.

### Full palette
| Hex | Role |
|---|---|
| `#061320` | Page background — deep navy (signature) |
| `#000D1D` | Deeper accent panels |
| `#FFFFFF` | Primary text |
| `#6199FF` | Brand link blue (CTAs, hover) |
| `#3860BE` / `#3B608D` | Secondary blue gradients |
| `#48576B` | Mid blue-grey (dividers) |
| `#B0BDC9` | Caption / meta text |
| `#F3F3F3` / `#E0E0E0` | Light surfaces (rare) |
| `#191C1E` | Card / tile dark grey |

Cinematic IMAX-theatre palette: dark navy is the canvas, blue accents glow, white type pops.

### Typography
- **Display headings (movie titles, section H2s):** `trumpsoftpro` — slab/serif hybrid, weights 400/500/700, italic variants. Carries the "blockbuster poster" feel.
- **UI / body:** `proxima-nova` weights 300/400/600/700 + italics.
- **Brand wordmark / fallback:** `gotham_book`, `gotham_medium`, `gotham_bold`.
- All section headers ("SPOTLIGHT", "LATEST NEWS") in all-caps with a thin horizontal `<hr>` rule under them — very editorial-newsroom.

### Nav structure
- **Header (transparent over hero):**
  - Left: Legendary globe icon + wordmark.
  - Center-left: FILM, TV, COMICS, NERDIST, LATEST NEWS, ABOUT, SHOP (uppercase, letter-spaced).
  - Right: IG, TikTok, X, FB, YT social icons.
- **No mega menu** — links go straight to top-level division pages.
- **Below hero:** SPOTLIGHT section (news carousel), then LATEST NEWS carousel with VIEW ALL link, then Catalogs grid.

### Footer
- Dark navy continues. Three-row layout:
  1. Social icon row (IG, TikTok, X, FB, YT — repeated from header).
  2. Utility links: CAREERS · PRIVACY · DO NOT SELL OR SHARE MY INFORMATION · TERMS · ABOUT.
  3. Long paragraph copyright/about block: "TM & © 2024 Legendary. All rights reserved. Legendary Entertainment is a leading media company with film... television and digital... and comics divisions dedicated to owning, producing and delivering content to mainstream audiences with a targeted focus on the powerful fandom demographic."
- No newsletter capture in footer (Legendary leans on social, not email).

---

## Patterns To Steal — Summary For Sullivan Mockups

### From Bieber
A **contained 16:9 video tile floated in generous negative space** (NOT full-bleed), framed by carousel chevrons, with a single elegant SVG play button — the video is a *click-to-launch* lightbox so the homepage stays still and editorial. For Sullivan, swap dusty pink for a luxury neutral (champagne, bone, deep oxblood, or midnight) and use the same pattern: still hero frame of him performing at a gala, big serif play icon, no autoplay noise, lightbox YT/Vimeo on click. Keeps the page feeling like a designed editorial spread, not a TV channel.

### From Chris Brown
A **monochromatic tonal palette** where the artist photo is *color-matched to the entire page* — wardrobe, background, and typography all share one warm temperature (chocolate × camel × cream). Hero is a **horizontal full-bleed editorial portrait** (reclining/lounging full-body, NOT a head-on bust) with type living in the left third and the subject on the right. For Sullivan: tuxedo black × champagne gold × cream, or midnight navy × brass × ivory. Shoot a cinematic full-body hero (mid-performance or lounging in formalwear in an event space), let his outfit echo the brand neutrals, run an ornate serif wordmark over the dark third and a thin sans CTA beneath. Carry one separate portrait crop for mobile rather than CSS-cropping.

### From Legendary
A **video-driven slide carousel (3 slides)** with native muted `<video>`, no audio ever, no player chrome — just a centered title in display serif + an outlined-pill "DISCOVER MORE" CTA bottom-center, dots below and chevrons on the sides. Transitions are *driven by video end events*, not timers, so each clip plays through fully before sliding. Critically: **separate portrait MP4s served to mobile**, with loop=true on mobile but autoplay-once on desktop. For Sullivan: 3 muted b-roll clips (gala entrance / live performance / crowd reaction) on a deep-navy or onyx page, white outlined CTA "Inquire About Booking" / "See Recent Events" / "Watch Reel" overlaid. Reads as a movie studio's reel, not a singer's merch store — exactly the luxury-events-company posture we want.

### File
`/Users/dioxmini/Projects/sullivan-fantastic-mockups/references/design-dna-round2.md`
