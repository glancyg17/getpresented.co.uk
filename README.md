# Get Presented. — Website Repo

Static site for **getpresented.co.uk**. Hosted on GitHub Pages, no build step — just plain HTML/CSS/JS files served directly.

## File structure

```
getpresented.co.uk/
├── index.html              ← Homepage
├── get-started.html        ← Step 1: persuasion page (ad lands here)
├── get-started-details.html ← Step 2: the intake form
├── thank-you-enquiry.html  ← Shown after form submission
├── privacy-policy.html     ← Privacy policy (no cookies used)
├── 404.html                ← Branded error page
├── sitemap.xml             ← Submitted to Google Search Console
├── robots.txt              ← Allows all crawlers, including AI bots
├── llms.txt                ← AI-readable business summary
├── CNAME                   ← Custom domain config for GitHub Pages
├── .gitignore
├── README.md                ← This file
└── assets/
    ├── icons/
    │   └── favicon.png     ← 512×512px
    └── images/
        └── og-image.jpg    ← 1200×630px, shown when link is shared
```

> **Note on file naming:** the pages above are named to match what they are. If matching the sitemap's clean URLs (`/get-started`, `/get-started/details`) rather than `.html` extensions matters, either rename to match GitHub Pages' extensionless routing conventions, or add redirects — flag this before final deploy.

## Brand basics

| Token | Value |
|---|---|
| Paper (background) | `#F7F3EC` |
| Ink (text) | `#211D17` |
| Rust (primary accent) | `#B5542E` |
| Rust dark (shadows/borders) | `#9A4423` |
| Green (success/secondary) | `#3D7A5C` |
| Line/border | `#D8CFBC` |
| Card | `#FAFAF8` |

**Fonts:** Fraunces (display/headings), Inter (body/UI), Space Mono (prices, labels, small caps), Caveat (handwritten accents, used sparingly).

## Making content edits

Each page is a single self-contained HTML file — CSS and JS are inline at the top/bottom of the file, no build step required. To edit copy, prices, or contact details:

1. Open the relevant `.html` file
2. Find the text directly in the markup (search for the visible English text, not a class name)
3. Edit and save
4. Commit and push to `main` — GitHub Pages rebuilds automatically, live in ~2 minutes

## Forms

The intake form (`get-started-details.html`) submits to **FormSubmit.co** at `hello@getpresented.co.uk`. FormSubmit requires a one-time confirmation click the first time it receives a real submission — check the inbox after the first live test.

Field names sent to your inbox are set via `name="..."` attributes on each input — keep these human-readable, since they become the email's field labels.

## Known placeholders to replace before launch

- [ ] `assets/icons/favicon.png` — currently a stub, needs real logo
- [ ] `assets/images/og-image.jpg` — currently a stub, needs branded design
- [ ] Portfolio carousel links/photos on homepage — currently point to real client sites (EK Van Services, Casa Mayis, Criterion Bids) but use placeholder image blocks, not real screenshots
- [ ] Final client quotes/site selection/order in the homepage carousel — flagged as a content decision, not yet finalised
- [ ] WhatsApp link in the homepage "talk" section currently a `#` placeholder — needs the real `wa.me/...` link

## Deploy checklist

See the full SOP doc for the complete pre-launch checklist (DNS, GitHub Pages setup, FormSubmit activation, Search Console submission). This README covers repo structure only.
