# william-contact

William Idoine's link and contact card. One static page, hosted free on GitHub Pages.
No build step, no framework, no third-party requests. A copy of
[XaviourG/xav-contact](https://github.com/XaviourG/xav-contact); keep the two in step.

Live: **https://vectorise-labs.github.io/william-contact/**

## What's in the box

```
index.html     The whole site: HTML + inline CSS + three small inline scripts
william.vcf    Static vCard the "Add contact" row shares / downloads
william.jpg    Headshot (480px square), from the marketing site's public/team/william-idoine.webp
favicon.svg    The Vectorise mark on black
fonts/         Anton, Geist + Geist Mono woff2, vendored (OFL). See fonts/SOURCE.md
.nojekyll      Tells GitHub Pages to serve files verbatim (no Jekyll)
```

## Design

The page follows the Vectorise design language (`DESIGN.md` in
`vectorise-labs/vectorise-labs-marketing-site`): black page `#0d0d0d`, square corners, hairline
rules instead of boxes, Anton for the name, Geist bold for sentences, Geist Mono caps for every
label, blue for the answer and orange only for the problem. Section markers (blue bar, label,
hairline, the Vectorise mark) open each section.

Order: identity, the LinkedIn button, the scaling roadmap panel, then Connect rows (Add contact,
Vectorise) and the Elsewhere grid.

The roadmap panel links to https://vectoriselabs.com/scaling-roadmap/ (tagged
`utm_source=william-contact`). Its canvas is a miniature of the site's bottleneck graphic: changes
flow through seven areas, bunch up and are lost at two orange bottlenecks (each named by its area, such as TESTING), then flush once the
bottlenecks lift to the team's stage. It pauses off screen and draws one still frame under
reduced motion.

## Links

| Where | URL |
|---|---|
| LinkedIn | https://linkedin.com/in/william-idoine |
| Email | william.idoine@vectoriselabs.com |
| GitHub | https://github.com/ILikeYourCode |
| Team health | https://developers.vectoriselabs.com/team-health |
| Vectorise | https://vectoriselabs.com |

## Edit your details

Contact values live in **two** places. Keep them in sync:

1. **`index.html`**: the links in `<main>`. Each is an anchor with an inline SVG icon,
   a mono label and a value.
2. **`william.vcf`**: the file the "Add contact" row shares. Plain vCard 3.0 with CRLF line
   endings. After editing, re-CRLF it:
   `perl -i -pe 's/\r?\n/\r\n/g' william.vcf`

### How the Add contact button works across platforms

| Environment | Path taken | UX |
|---|---|---|
| iOS Safari 16+ | JS upgrades the click to `navigator.share({ files: [vcf] })` | Native iOS share sheet opens with **Save to Contacts** as a first-class option |
| Android Chrome | Same `navigator.share()` path (Web Share API Level 2) | Native Android share sheet, then Contacts |
| Desktop / older iOS / unsupported browsers | The anchor's `href="william.vcf"` runs unchanged | Browser downloads the file; user opens it in Contacts |

The single static `william.vcf` is the source of truth for both paths.

## Deploy

Push to `main`. GitHub Pages serves the repository root over HTTPS.
