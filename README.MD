# Client Brief #01 — Ceramics Studio

**"Adel & Co. Ceramics" is not a real business.** This project is built from a simulated client brief (see [BRIEF.md](./BRIEF.md)), written to read like a real early-stage freelance engagement: a written brief, no existing brand assets, a vague aesthetic direction to translate into real design decisions. This is practice, not client work, and it's presented as exactly that. First in a series of client-brief practice projects.

**Live demo:** https://tarek-elzoghby.github.io/client-brief-01-ceramics-studio/ *(pending verification once Pages is enabled on this account)*

## What it does

A one-page static site for a fictional potter, Marwa, who wants a simple page to send people to instead of managing everything through Instagram DMs. Hero, about, gallery, and contact sections, built entirely from the brief's requirements: warm and handmade, not corporate, mobile-first since most visitors would arrive from Instagram on a phone.

## Why I built it this way

The brief's only real direction was a feeling: "not like a SaaS startup page." Before writing any code, I worked out what that meant concretely. Landed on a "Clay Light" direction: warm, slightly imperfect, closer to walking into a studio than opening an app. Over-polished, grid-perfect SaaS precision would have undermined trust for something this personal, so warm and human became the credibility signal instead of slickness.

That decision drove everything downstream. Fraunces for headings (soft, low-contrast letterforms) paired with Karla for body text, deliberately not Inter, since that reads as generic SaaS. A clay and terracotta palette with one accent color (#B5603F), the actual color of fired clay, so it works as both brand color and material reference. No blue, no white, no black anywhere in the system.

I decided against a nav bar. One page, one path, and nav bars read as "website" in a way that fights the whole feeling. A quiet scroll indicator does that job instead, built as a real anchor link so it's accessible, not decorative. Working out where it belonged took some back and forth: a `<header>` is for introductory content, and a scroll cue isn't introducing anything, it's pointing at what comes next. It ended up living inside the hero section itself, since that's the section it actually belongs to.

## Tech

Plain HTML and CSS. No framework, no build step. The site doesn't need one, so it doesn't have one.

## Running it locally

```
git clone https://github.com/Tarek-Elzoghby/client-brief-01-ceramics-studio.git
cd client-brief-01-ceramics-studio
open index.html
```

No install, no build step.

## Accessibility

Ran a Lighthouse pass after the build: 99 Performance, 95 Accessibility, 100 Best Practices, 91 SEO. The contact links were flagged for low contrast, terracotta on cream was sitting around 3.9:1, just under the AA threshold for normal-size text. Fixed by swapping to a darker shade already in the palette. Accessibility went to 100 after that one change.

Other choices made with keyboard and screen reader use in mind: visible `:focus-visible` outlines on links instead of relying on the browser default, `loading="lazy"` on gallery images since they sit below the fold, descriptive alt text on every gallery item, and a real anchor link (not a decorative arrow) for the scroll indicator.

## Known issues and what's next

- Gallery uses placeholder images. Real studio photos come once the (fictional) client sends them.
- Hero background is currently a soft radial gradient rather than a photo, intentional for now since a stock pottery image would misrepresent the studio's actual work. Once real photos exist, the plan is a low-opacity hero photo, and the current gradient moves down to become the About section's background.

## Status

Built and reviewed. Not yet deployed.
