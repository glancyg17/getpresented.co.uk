# getPresented. (UK) — working codex

*Living document. Last updated: 24 October 2026.*
**Rule: if reality changes (a price, a link, a page, a decision), update this file in the same commit.** Read it before working on this repo.

> **Public-repo warning.** This repo is public and `_config.yml` only hides this file from the *published site*, not from GitHub. Keep anything private out of it: internal pricing strategy, ad budgets and targeting, revenue goals, client personal data, the forwarding Gmail address, API keys. Private strategy lives in the Claude Project's codex, not here.

---

## 1. What this is

**getPresented.** is a solo web-services business run by **Glancy**: simple, fast, fairly priced websites for UK tradespeople and small local businesses, plus branding add-ons. The brand's promise is **a website you never have to touch, run by a real person you can message.** This repo is the UK marketing and sales site (getpresented.co.uk), static HTML on GitHub Pages, no build step.

A separate sister brand, **preséntame.** (Mexico/LATAM), has its own repo (`presentame.online`), built from this template. Changes made here do not automatically apply there; check before copying.

- UK email: `hello@getpresented.co.uk`
- UK WhatsApp: +44 7301 222435 (`https://wa.me/447301222435`). It is also the **edit line** for existing clients.

## 2. Products and pricing (UK, GBP)

### Billing mechanics (verified in Stripe, Oct 2026)
Every site bundle is **one-off build fee + £10/month hosting, with the first month taken at checkout.** So the **first payment = build fee + £10**, then £10/month from month 2. There is **no free hosting month and no 30-day trial**. (A stale `trial_period_days: 30` setting exists on the shared £10 hosting price in Stripe. Checkout ignores it, but don't rely on it, and don't write "from day 30" anywhere.)

### Sites
| Product | Build | Monthly | First payment | Link |
|---|---|---|---|---|
| Simple Website + Hosting (**Live**) | £50 | £10 | **£60** | https://buy.stripe.com/aFa14m0To4QD7Fy9YC9EI0c |
| Simple Website + Fresh | £50 | £20 | **£70** | https://buy.stripe.com/4gM8wOby23Mz5xq0o29EI0o |
| Simple Website (build only, own hosting) | £50 | — | £50 | https://buy.stripe.com/6oU9ASatYcj5f802wa9EI06 |
| WordPress site | £100–£150, quoted | — | — | no link |
| Custom builds | £149 / £199 / £249 | — | same | https://buy.stripe.com/9B65kC59E82P0d64Ei9EI09 · https://buy.stripe.com/dRm9AS59E4QDaRK1s69EI0a · https://buy.stripe.com/cNi3cu6dI6YLaRK2wa9EI0b |

### Monthly plans
| Plan | Price | Includes |
|---|---|---|
| **Live** | £10/mo | Hosting, domain management, **2 changes a month by message**, cancel any time |
| **Fresh** | £20/mo | Everything in Live, **unlimited everyday changes by message**, **monthly "how your site did" message**, **seasonal nudges (4/yr)**, **yearly check-up + flyer/card/menu refresh**. Process: `docs/fresh-service.md` |

Standalone links: Hosting £10/mo https://buy.stripe.com/28E4gy31werd9NG1s69EI07 · **Upgrade to Fresh** £20/mo `https://buy.stripe.com/fZu6oGgSm0An2le6Mq9EI0p` (when someone upgrades from Live, **cancel their old £10 subscription** in Stripe).

A **"change"** = one request (one topic: new hours, a swapped photo, an updated price list). Full definition, scope and process: `docs/edit-workflow.md`.

### Branding (fixed prices, buy-now on `/branding/`)
| Product | Price | Contents |
|---|---|---|
| Starter Identity | £50 | Logo, palette, type pairing, favicon, business card |
| Social Identity | £50 | WhatsApp Business assets, email signature, social images/banners, flyer, QR |
| Full Identity | £75 | Starter + Social |
| Menu Design | £35 flat | Print-ready menu |

Links: Starter https://buy.stripe.com/00w5kCfOi3Mz1ha2wa9EI0h · Social https://buy.stripe.com/bJe6oG45Adn92le9YC9EI0i · Full https://buy.stripe.com/eVq5kC59E5UH3pi4Ei9EI0j · Menu https://buy.stripe.com/8x214mgSmgzlbVO2wa9EI0k

### Site + branding bundles (hosting included; sold via WhatsApp "Ask about this", not a buy button)
| Bundle | Build | First payment | Then |
|---|---|---|---|
| Site + Starter Identity | £75 | £85 | £10/mo |
| Site + Social Identity | £75 | £85 | £10/mo |
| **Properly Presented** (site + Full Identity) | £99 | £109 | £10/mo, **includes first 3 months of Fresh-level service** |

Properly Presented's Fresh months are a **service perk, not a billing change**: the client pays £10/mo throughout and gets unlimited everyday changes for 3 months; offer the £20 upgrade at the end.

Other: **domain transfer £17** if a client leaves (https://buy.stripe.com/bJe8wO1Xs0An7Fy9YC9EI08). No formal contract. Non-payment → site suspended.

### Pricing messaging rules
- Lead with the bundle: *"£50 to build, then £10 a month to keep it live."*
- Primary CTAs use benefit language ("Build my site"), no prices on buttons.
- Ads say **"from £50"** (leaves room for £100–£350 custom jobs).
- **Do not publish** "price never goes up", "price-lock", or any promise that restricts future price rises. **Do not publish** a response-time promise until one is decided (see edit-workflow §2).

## 3. Client flow (UK)

```
Ad / search / referral → getpresented.co.uk
→ /get-started (persuasion) → /get-started/details (intake form, FormSubmit) — or WhatsApp
→ /thank-you-enquiry
→ Glancy reviews → WhatsApp conversation → Stripe link sent in chat
→ /payment-confirmed/<product>/
→ build → handover message → client uses WhatsApp for changes
```
Some products pay first (branding "Buy now", Simple Website + Fresh) and collect details on the confirmation page. Clients send logo/photos by WhatsApp or email; there is no upload form.

## 4. Repo map

```
index.html                 Homepage: hero demo, work carousel, "Text us" chat demo, plans, process, branding teaser, solutions teaser
branding/index.html        Standalone identity products (buy buttons) + site bundles (WhatsApp ask)
get-started/index.html     Persuasion page
get-started/details/       Intake form (FormSubmit)
thank-you-enquiry/         Fires Lead
solutions/                 Bespoke software page
privacy-policy/            Discloses Meta Pixel + consent banner
payment-confirmed/<slug>/  One page per Stripe link (see §6). /payment-confirmed/index.html is the generic £50 fallback
404.html · sitemap.xml · robots.txt · llms.txt · CNAME · _config.yml
assets/icons/ assets/images/   (gallery: orbitvision, rfstrategic, kennedy, mayatuya, steviemacs, ekvan; plus og-image, logo)
docs/                      Internal process docs (edit-workflow.md, client-site-CLAUDE-template.md)
```
Each HTML page is self-contained (inline CSS/JS). Edit visible copy directly; no build step. Push to `main` → live in ~2 minutes.

## 5. Design system

| Token | Value | Use |
|---|---|---|
| Paper | `#F7F3EC` | Background |
| Ink | `#211D17` | Text |
| Rust | `#B5542E` | Accent, CTAs, the dot |
| Rust Dark | `#9A4423` | Button shadows/borders |
| Green | `#3D7A5C` | Success, ticks |
| Line | `#D8CFBC` | Borders |
| Card | `#FAFAF8` | Cards |
| Soft | `#5C5648` | Secondary text |

Fonts (Google): **Fraunces** headings, **Inter** body, **Space Mono** labels/prices, **Caveat** handwritten accents (sparingly). Wordmark `getPresented.` in Fraunces Bold with a rust dot. Tagline: *"Your business, online. Properly."*
Voice: plain, direct, British English, sentence case, no jargon, no hype. Say what happens.
The nav is sticky; motion respects `prefers-reduced-motion`. Mobile-first.

## 6. Tracking and the Meta Pixel (do not break)

- **UK dataset ID `866982179477687`.** The MX site uses a **different** dataset; never cross-wire when cloning.
- Pixel loads only after consent via the `#fp-consent` banner (Accept/Decline), stored in `localStorage` key `fp_ad_consent`. This block is copied verbatim into every page. **Never edit it, and always include it on new pages.**
- Events: `PageView` (all pages) · `Lead` (thank-you page load and WhatsApp button `onclick`) · `InitiateCheckout` (branding buy buttons and the homepage "Build my site with Fresh" button) · `Purchase` (confirmation pages, value = **actual first payment**).

| Confirmation page | Purchase value |
|---|---|
| `/payment-confirmed/` (generic) · `simple-website` | £50 |
| `site-hosting` (Live) | £60 |
| `site-fresh` | £70 |
| `fresh` (upgrade) | £20 |
| `hosting` | £10 |
| `starter-identity` · `social-identity` | £50 |
| `full-identity` | £75 |
| `menu-design` | £35 |
| `site-starter-identity` · `site-social-identity` | £85 |
| `properly-presented` | £109 |
| `custom-149` / `-199` / `-249` | £149 / £199 / £249 |
| `domain-transfer` | £17 |

Confirmation pages are `noindex`. **When a Stripe link is created or its price changes, create/update its confirmation page and its Purchase value.**
Forms: the intake form posts to FormSubmit.co (destination is an alias configured in the form; don't write the destination address in this file).
Analytics: **Umami Cloud** (cookie-free, no consent needed). The tag sits in `<head>` of every page, with `data-domains="getpresented.co.uk"` so local previews and the github.io mirror don't count. Include it on every new page. MX needs its **own** Umami website ID; never reuse this one.

## 7. SEO

Every page has title, description, robots, canonical, Open Graph and Twitter tags. Non-indexable: details, thank-you, all confirmation pages. `robots.txt` allows all crawlers including AI bots; `llms.txt` is the AI-readable summary and **must match current pricing**. Update `sitemap.xml` `lastmod` when a page's content changes.

## 8. Working rules for Claude in this repo

1. **Preserve** the consent/Pixel block, WhatsApp `onclick="…fbq('track','Lead')…"` handlers, meta tags and Stripe links unless the task says otherwise.
2. After any pricing change, grep the whole repo for the old number and update: homepage, `get-started`, `branding`, `llms.txt`, confirmation pages, meta descriptions, and this file.
3. Never write "from day 30", "first month free", or "price never goes up".
4. New product → new Stripe link (in Stripe), new `/payment-confirmed/<slug>/` page from an existing one, correct Purchase value, entry in §2 and §6 here. No payment-link URLs from memory: copy them from Stripe or this file.
5. Match the visual language already on the page. Reuse tokens; don't add new colours or fonts.
6. Check `<div>` balance, anchors and mobile width after edits. Every page needs the Umami tag in `<head>` and (except 404, privacy policy) the consent/Pixel block.
7. Don't add customer names, emails, phone numbers or screenshots of payments to the repo.
8. Edit requests from clients follow `docs/edit-workflow.md`.
9. **Writing style:** the copy must sound like one person talking, not a brochure. **No em dashes** in site copy (use a full stop, a comma, a colon or brackets). Page titles use ` | ` as the separator. Avoid "not X, it's Y" constructions, neat lists of three, and filler like "no surprises", "seamless" or "tailored". Short sentences, plain words, say what happens.

## 9. Marketing status (public-safe summary)

- **UK:** site live and tracked; ad creative built (6-frame video, order 1+2 → 3 → 5 → 4 → 6); paid campaign deprioritised. Growth is manual/referral for now.
- **Meta platform notes:** detailed interest targeting is gone (Advantage+ Audience only); learning phase needs roughly 50 conversions/week on the optimisation event, so small always-on budgets stay "Learning limited".

## 10. Open items

- [ ] **Response-time promise** for message edits (recommended: "by the end of the next working day"); then add to site.
- [ ] **Privacy policy**: add a line on WhatsApp messages/photos/voice notes handled for edit requests (what is kept, for how long).
- [ ] Carousel quotes for Kennedy and Maya Tuya are still placeholders; need real client words. Orbit Vision, RF Strategic and Stevie Macs quotes are client-approved wording, temporary; all five are marked `TEMP quote` in `index.html`: replace with Google reviews. Casa Mayis is MX-only and is not in the UK gallery.
- [ ] **Fresh pulse is now promised on the site.** Before the first Fresh client reaches month 2: set up Cloudflare Web Analytics + Search Console for each client site (SOP), and test one pulse end to end (`docs/fresh-service.md`).
- [ ] Rebrand Gmail canned responses A–E; write Template F (consider a WhatsApp-format scope + payment message).
- [ ] Clean up the stale 30-day trial setting on the £10 hosting price in Stripe (create a new price, don't edit the old one).
- [ ] Stripe account display name → `getPresented.`; Google Search Console; GBP listing; social bio links.
- [ ] README placeholders were replaced; keep README short and point here.
- [ ] Decide whether older confirmation pages (`simple-website`, generic) should mention edits.

## 11. Decisions log (newest first)

- **24 Oct 2026**: Site refocused on "a website you never have to touch": edits by WhatsApp. Plans: **Live £10** (2 changes/mo) and **Fresh £20** (unlimited everyday changes + yearly collateral refresh). Fresh and Upgrade links created in Stripe. Properly Presented includes 3 months of Fresh-level service (perk, no billing change).
- **24 Oct 2026**: Confirmed billing is £60 first payment (build + first month). Removed all "from day 30 / first month free" claims; corrected Purchase values (£60/£70/£85/£109).
- **24 Oct 2026**: Umami installed on all pages (cookie-free; domain-restricted to getpresented.co.uk). Resolves the privacy-policy mismatch.
- **24 Oct 2026**: Added `docs/edit-workflow.md`, client repo `CLAUDE.md` template, `_config.yml` exclude, and this file.
- **Sept 2026**: Branding catalogue added (Starter £50, Social £50, Full £75, Menu £35 flat) with three site bundles; hosting standard in bundles because the monthly residual is the business.
- **Aug 2026**: Meta Pixel added (consent-gated), privacy policy rewritten to match; UK paid campaign paused; MX prioritised for ad spend (see MX repo).
- **June 2026**: Rebrand presentame. → getPresented. (UK). Static-site rebuild; bundle pricing; no live chat widget.

## 12. Mexico (preséntame.) — pointers only

Separate repo and domain (`presentame.online`), Spanish, MXN, WhatsApp-first funnel via click-to-WhatsApp ads, separate Pixel dataset. A price increase for MX hosting and the Fresh equivalent has been decided in principle but not implemented; take figures from the MX repo's own file, not from here.
