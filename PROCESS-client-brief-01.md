# How this site was built

The reasoning behind the design and build decisions for Adel & Co. Ceramics — a one-page site for a potter, built from a simulated client brief.

## Starting point

The brief: a potter with no technical background and no existing site, managing commissions through Instagram DMs, needing a simple one-page site. No brand system existed yet — just a feeling to design toward: not a SaaS startup page.

## Finding the direction: "Clay Light"

Before any code, the visual direction came first. The reasoning: over-polished SaaS precision — perfect grids, cold sans fonts, blue gradients — actually undermines trust for something as personal as commissioning handmade pottery. Warm and slightly imperfect, more like walking into a real studio than opening an app, was the actual credibility signal here, not slickness.

That decision shaped everything downstream:

- **Typography** — Fraunces for display (soft, low-contrast, slightly hand-drawn letterforms) paired with Karla for body. Deliberately not Inter, which is the fastest route back to generic SaaS.
- **Color** — a warm clay/beige palette with a single terracotta accent (`#B5603F`), chosen because it's literally the color of fired clay — it doubles as brand color and material reference at once. No blue, no white, no black anywhere in the system.
- **Spacing** — an 8px base unit with generous section padding (64–128px), so scrolling feels like moving room to room in a studio rather than a scroll-jacked landing page.

## No nav bar, on purpose

One page, one path — a nav bar reads as "Website" in a way that fights the Clay Light feeling. A quiet scroll indicator replaces it instead, built as a real anchor link so it stays functional, not just decorative.

## Where does a scroll indicator actually live?

It wasn't obviously part of any existing structural unit. A `<header>` is for introductory content, and a scroll cue isn't introducing anything — it's pointing at what comes next. It also didn't belong loose in `<main>`, since it wasn't tied to a section. The resolution: it isn't its own structural unit at all — it's part of the hero's job, so it lives inside the hero section, right after the tagline.

Reviewing the build against that plan caught a mismatch: the first pass had built a `<progress>` scroll-bar instead of the anchor-link chevron. A progress bar tracks page-scroll position and needs JavaScript — a different feature entirely from a "there's more below, tap here" cue. Went back to the actual plan: a plain anchor link inside the hero.

## space-between vs. space-around

The hero uses `justify-content: space-between` to keep the heading tight at the top and the scroll indicator pinned to the bottom. The instinct was to reach for `space-around` to keep things off the edges, but both properties distribute *leftover* space between children — `space-around` even gives half-size gaps at the edges compared to between items, which isn't the intuitive read. Padding is the right tool for guaranteed edge distance, since it's a fixed value that won't shift if content height changes later. Two separate jobs: padding controls edge distance, justify-content controls how children are spaced from each other.

## Keeping the rhythm consistent

Vertical section padding stays identical (64px → 128px) across every section — that consistency is what creates the "room to room" feeling. Horizontal padding also stays fixed for edge safety, but the content width inside each section varies with what it's showing: About gets a narrow 720px reading column, Gallery goes wider (~1100px) since it's image-based rather than prose.

## About: left-aligned, not centered

Centered paragraphs are harder to scan — the eye has to hunt for each new line's start. Left-alignment inside a centered wrapper also created a deliberate rhythm shift across the page: the hero reads as signage (centered, symmetrical), About reads as a conversation (left-aligned, intimate).

## Two quiet bugs, same root cause

`content: '↓'` did nothing — that property only applies to `::before`/`::after`, not regular elements. Fixed by placing the arrow directly in the markup. Right after, the anchor link wasn't scrolling anywhere — the target section had been given a class instead of an id, and fragment links only match ids. Both bugs were the sneaky kind: nothing visibly broken, nothing happening either.

## Building the gallery grid

The first section that needed real structural thinking. CSS Grid over Flexbox, since Grid handles rows and columns as one system. `repeat(auto-fit, minmax(220px, 1fr))` lets the column count adjust to screen width with no breakpoints needed. Every item is forced to a 1:1 ratio with `object-fit: cover`, so the grid stays visually calm once real, differently-shaped photos replace the current placeholders — sourced from placehold.co to avoid copyright risk and match the palette while real photos aren't available yet.

Two small bugs on first pass: the grid wasn't centered (`margin-inline: auto` was missing — `max-width` alone doesn't center anything), and images weren't filling their squares (`object-fit: cover` had nothing to cover into without explicit `width`/`height: 100%` on the image). Both fixed, and the grid read correctly immediately after.

## Contact icons: inline SVG, not emoji or images

Emoji can't be recolored and clash with the palette; `<img>`-based icons lose the ability to control color via CSS. Inline SVG with `stroke="currentColor"` lets the existing color variables control icon color directly. Each row groups icon and label tightly, with a larger gap before the value — the value is the only real tap target, styled in terracotta since that's the one accent reserved for actual calls-to-action.

## Fixing a hero that felt flat

Once all four sections existed and the page was reviewed as a whole, the hero felt too empty — a lot of warm beige with centered text and nothing else. A background photo was the obvious fix, but would have meant a generic stock pottery image, working against the entire "credible, real person" feeling the site is built around. A subtle radial gradient (`--color-surface` fading into `--color-background`, centered behind the text) solved it instead. A CSS-only grain texture was also tried on top of the gradient, using an SVG `feTurbulence` filter with no image file needed — but the gradient alone did the job, so the extra layer was dropped. No reason to stack two tricks when one already works.

## What's planned, not yet built

Once real studio photos exist, a low-opacity photo goes behind the hero text — not sooner, since a placeholder or stock photo would misrepresent the actual work. Once the hero moves to a real photo, the radial-gradient technique moves down to become About's background instead. The instinct was initially "don't repeat the same visual trick twice" — but a photo and a soft gradient don't actually read as the same thing to a viewer, even with a similar CSS mechanism underneath. Reusing the technique there isn't a repeat, it's reusing a tool for a different job.

One incidental benefit: the mobile layout already leaves a gap between the tight heading block and the bottom-pinned scroll indicator — a side effect of the `space-between` decision made purely for spacing reasons early on. That's exactly the space a future hero photo will slot into with no layout changes needed.

## Accessibility and performance pass

A dedicated pass followed the initial build, checking production-readiness rather than just visual polish. A Lighthouse baseline came back strong for a static single-page site: 99 Performance, 95 Accessibility, 100 Best Practices, 91 SEO.

From there: `loading="lazy"` added to gallery images, since they sit below the fold and don't need to load on initial view. `:focus-visible` outline styling added on links, using terracotta instead of the default browser blue, so keyboard users get a real visible focus indicator without a mouse-click ring appearing unnecessarily. Underlines on contact-value links stay off at rest for a cleaner look, but return on hover/focus, so there's still a non-color signal that the text is clickable.

Lighthouse flagged the three contact-value links for low color contrast — terracotta on cream was sitting around 3.9:1, just under the 4.5:1 AA threshold for normal text. Fixed by swapping to `--color-primary-dark`, a shade already in the palette originally meant for a hover state, which cleared contrast comfortably while staying on-brand. Accessibility score reached 100 after that single change.

SEO was left as-is for now — the remaining points are mostly meta-description and content-dependent, and better addressed once real client copy and images are in.
