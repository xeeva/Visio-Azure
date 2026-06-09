---
layout: default
title: Sponsorship
---

# Sponsorship

## Why this is set up the way it is

The previous Azure-Design repo (now archived) distributed every icon as both a `.vssx` stencil **and** loose `.svg` / `.png` files. The intention was simple: give the community what it asked for. The reality turned out differently. The loose SVG and PNG files were systematically scraped, re-hosted on third-party design-asset sites, and used in commercial products without attribution. The licence required only that the source be acknowledged. That was repeatedly ignored.

To keep this project maintainable without effectively giving the work away to people who strip attribution and resell it, the V-5.0 release splits delivery in two:

- **Free, in this public repo:** the `.vssx` stencils. The full collection. Everything you need to actually use the icons inside Visio for free, forever, under GPL-3.
- **Sponsor-only, in a private repo:** the per-icon `.svg` and `.png` asset files, plus the un-watermarked preview image.

If all you need is Visio, you never need to sponsor anything. The stencils are complete.

If you build slide decks, websites, marketing materials, or anything that consumes the icons as standalone files outside Visio -- the SVG / PNG library is where you find them.

## Tiers

| Tier | Price | What you get |
| --- | --- | --- |
| **Supporter** | $3 / month | Read access to the [Visio-Azure-Premium](https://github.com/xeeva/Visio-Azure-Premium) private repo: per-icon SVGs, two PNG resolutions (256 px and 1024 px), the un-watermarked preview, and early access to new releases |
| **Studio** | $15 / month | Supporter access + a one-line commercial-use clearance covering teams of up to 25 -- means you can drop the icons into client deliverables without per-seat licensing concerns |
| **Enterprise** | $50 / month | Studio + priority on icon-request triage (new Azure services, custom variants) and a named credit in the release notes |
| One-off support | Any amount | Pay-what-you-want one-time tier on GitHub Sponsors -- gets you a thank-you and the warm glow of supporting open infrastructure |

[Sponsor on GitHub →](https://github.com/sponsors/xeeva){: .btn }

## How access works

1. **Sponsor at any paid tier** via [github.com/sponsors/xeeva](https://github.com/sponsors/xeeva).
2. **Send a request** -- email the GitHub username you sponsored under to `david@xeeva.com.au`, or comment on the `Visio-Azure-Premium` repo access issue (`github.com/xeeva/Visio-Azure-Premium/issues/1`). Confirms the GitHub identity matches the sponsorship.
3. **Get added** -- within 24 hours you'll receive a GitHub invitation to collaborate on the private repo with **read** access. Clone, download, use.
4. **Ongoing while sponsorship is active** -- access stays as long as the sponsorship is active. Cancelling removes access at the end of the paid period; you keep anything you've already downloaded under the terms of the licence.

## What's in the premium repo

```
Visio-Azure-Premium/
├── V-5.0/
│   ├── svg/                          # 1,773 individual .svg files
│   │   ├── AI_Azure-OpenAI.svg
│   │   ├── ...
│   ├── png-256/                      # 256 px renders
│   │   ├── AI_Azure-OpenAI.png
│   │   ├── ...
│   ├── png-1024/                     # 1024 px renders
│   │   └── ...
│   └── preview-unwatermarked.png     # the full grid PNG, no watermark
├── V-4.7-legacy/                     # the legacy collection's SVG/PNG
└── README.md                         # attribution and licensing reminder
```

Each release is in its own folder. New versions land here a week or two before they're tagged on the public repo, so sponsors get early access.

## Licence on the asset files

The SVG and PNG files are the same icons rendered to standalone formats. The licence is the same -- **GPL-3.0** for the build pipeline, plus the Microsoft Azure icon usage terms (free for use in diagrams; attribution to Microsoft for the icon design). The premium part is **distribution access**, not a different licence. You can use the assets in commercial work; you have to keep attribution to both Microsoft (icon design) and this project (the normalisation / packaging work).

The Studio tier adds a clearance letter covering teams of up to 25 designers -- not a legal change, just a written confirmation you can drop into a procurement review without escalating.

## Why a private repo, not Polar/Gumroad

GitHub Sponsors is already integrated with GitHub identity, which is the same identity that pulls from a private repo. The flow is one-step:

- Sponsor → confirm GitHub username → repo invite arrives → `git clone`.

No download codes, no separate accounts, no email-link expiry. And updates land via `git pull`.

If you specifically prefer a one-off purchase over a subscription, [open a discussion](https://github.com/xeeva/Visio-Azure/discussions) -- I'm happy to set up a Polar.sh listing for the lifetime-access bundle if there's demand.

## Thank you

This project, and the legacy Azure-Design stencils it builds on, exists because people sponsor the maintenance. If you've used the icons in production work, please consider supporting the upkeep.

[Sponsor →](https://github.com/sponsors/xeeva){: .btn }
