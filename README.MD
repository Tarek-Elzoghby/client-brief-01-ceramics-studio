# Client Brief #01 — Ceramics Studio

A one-page studio site built from a simulated client brief, practicing what a real early-stage freelance engagement looks like: a vague aesthetic direction, no existing brand assets, and a written brief to translate into actual design decisions.

**"Adel & Co. Ceramics" is not a real business.** The brief (included as [BRIEF.md](./BRIEF.md)) was written to imitate one — right down to placeholder contact info — so this repo is practice, not client work, and it's presented as exactly that. First in a series of client-brief practice projects.

**Live demo:** https://tesidrah.github.io/client-brief-01-ceramics-studio/

## What this is

The brief: a potter in Cairo who's tired of managing commissions through Instagram DMs and wants a simple, credible one-page site instead — warm and handmade, explicitly "not like a SaaS startup page." This is the result: a static one-page site — hero, about, gallery, contact — built entirely from that brief.

## Design approach

Landed on a "Clay Light" direction: warm, slightly imperfect, closer to walking into a studio than opening an app. Fraunces (display) paired with Karla (body), a clay/terracotta palette with a single accent color, generous section padding for a "room to room" scroll feel, and a CSS Grid gallery that adjusts column count on its own — no breakpoints needed. No nav bar — one page, one path — replaced with a quiet scroll indicator built as a real, accessible anchor link rather than a decorative one.

## Accessibility & performance

Ran a Lighthouse pass after the build: 99 Performance, 95 Accessibility, 100 Best Practices, 91 SEO. One contrast issue was caught on the contact links (terracotta on cream, ~3.9:1) and fixed by swapping to a darker shade already in the palette — Accessibility went to 100 after that single change.

## Stack

Plain HTML and CSS. No framework, no build step — the site doesn't need one, so it doesn't have one.

## Running it locally

```
git clone https://github.com/TeSidrah/client-brief-01-ceramics-studio.git
cd client-brief-01-ceramics-studio
open index.html
```

No install, no build step.

## Status

Built and reviewed. Not yet deployed. Gallery uses placeholder images, per the brief.