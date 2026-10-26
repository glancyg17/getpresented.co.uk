# Edit workflow: "Text us. It's updated."

How a client's WhatsApp message becomes a live change. Written for Glancy and for Claude.
Status: **proposal, v1 (24 Oct 2026).** Items marked ⚠️ need a decision. Update this file as the process settles.

## 1. What the client is promised

| Plan | Price | Message-edits |
|---|---|---|
| Live | £10/mo | 2 changes a month |
| Fresh | £20/mo | Unlimited everyday changes, monthly pulse message, seasonal nudges, yearly check-up + flyer/card/menu refresh (see `docs/fresh-service.md`) |
| Properly Presented | £99 + £10/mo | Fresh-level service for the first 3 months, then Live (or upgrade to Fresh) |

**A "change" is one request**: a message (or short back-and-forth) about one thing, such as new opening hours, a swapped photo, an updated price list or a seasonal banner. A few small related tweaks in one message count as one.

**Everyday change** (included): text, prices, hours, contact details, swapping or adding photos, adding or removing a service line, updating a menu or price list, a temporary notice.

**Not included, quote separately:** a new page, a new section type or feature (booking form, shop, gallery rebuild), a redesign, integrations, branding work (see the branding catalogue), anything that needs real build time. Custom builds start at £149 (£149 / £199 / £249 links exist), or quote per job.

**Fresh fair use (internal, not published):** "unlimited" means reasonable. If a Fresh client sends more than about 4 requests a week for two months running, have a friendly chat about scope. Do not enforce mid-month or by surprise.

**Public wording** already on the homepage: *"A 'change' is one request, like new opening hours, a swapped photo or an updated price list. 'Unlimited' on Fresh means everyday changes to your existing pages. New pages or a redesign are quoted separately."*

## 2. Turnaround ⚠️

The site makes **no** response-time promise yet. Recommended: **"by the end of the next working day"**, which you can keep through weekends, illness and travel. Avoid "24 hours". Decide before adding it to the site. Once decided, record it in `CLAUDE.md`.

## 3. The workflow

```
WhatsApp message / photo / voice note
→ 1 Verify sender
→ 2 Classify (everyday / out of scope) and count against the plan
→ 3 Write an edit brief
→ 4 Claude makes the change in that client's repo
→ 5 Review the diff (preview if it touches layout or money)
→ 6 Push → GitHub Pages rebuilds (~2 min) → check it live
→ 7 Reply with the link
→ 8 Log it
```

### 1. Verify the sender
Only act on requests from the WhatsApp number on file for that client. A message from an unknown number, or a request that sounds off, gets a call-back or a check on the number on file before anything changes.
**Always confirm back before changing:** phone numbers, email addresses, payment or bank details, links that send customers somewhere else, domain or DNS anything. ("Just checking, change your phone number to 07xxx?") Impersonation is the main risk of an edit-by-message service, and a changed phone number or link is how it would bite.

### 2. Classify and count
- Find the client and plan (client list: see §4).
- Everyday change → continue. Out of scope → reply with a plain "that's a bigger job, here's the price" message, quote, and stop.
- Live client over 2 changes in a month: do not charge by default. Do it, then offer: "You update often, Fresh is £20 for unlimited. Want to switch?" (Option if you ever want one: a small per-change fee. Not recommended while you are learning how much time edits take.)

### 3. Edit brief
Turn the message into a short written brief before touching code:
- **What:** exact new text, prices, hours or photo (quote the client's words).
- **Where:** page and section.
- **Anything unclear:** ask one question on WhatsApp rather than guess.
- Voice notes: use WhatsApp's built-in transcript if available, otherwise listen and type the brief yourself. Check numbers and prices twice. Never change a price from a voice note without reading it back.

### 4. Make the change (Claude)
Open the client's site repo in Claude Code (or upload the file(s) to Claude) with the client's `CLAUDE.md` (template: `docs/client-site-CLAUDE-template.md`). Give Claude the brief. Rules for Claude:
- Change only what the brief says. No drive-by edits.
- Keep the client's design tokens, fonts and structure.
- Photos: compress first (Squoosh), sensible filenames, save under `assets/images/`, add real alt text, set width and height or a fixed aspect ratio.
- Update `sitemap.xml` `lastmod` only when page content changes.
- Never touch tracking, form endpoints or DNS files unless the brief says so.
- Show the diff and summarise it in plain English.

### 5. Review
- Text-only change: read the diff.
- Layout, prices, hours, links or photos: preview locally (`python3 -m http.server` in the repo) and check on a phone-width window.

### 6. Push and verify
Commit with a message in the form `edit: <client> <short description>`, push to `main`, wait about 2 minutes, then open the live URL and check the change (and that nothing else moved).

### 7. Reply
Short, human, include the link:
- *"Done ✅ New hours are live, have a look: example.co.uk"*
- *"Done ✅ Photo added to the homepage and gallery. Let me know if you'd like it cropped differently."*
- Out of scope: *"That's more than a quick change (it's a new page), but happy to do it. It'd be £xx. Want me to go ahead?"*
- Live client hitting the limit: *"All done ✅ That's your 2 for the month. If you update a lot, Fresh (£20/mo) gives you unlimited, just say the word."*

### 8. Log
One row per request in a simple sheet (or `EDITS.md` in each client repo): **Client · Date · Request · Counts toward allowance (Y/N) · Minutes spent.** Minutes is the important column. After about 20 edits you will know whether £10 and £20 are priced right.

## 4. The client list

Keep one row per client in a private place (not in a public repo): **Client · WhatsApp number on file · Plan · Repo · Domain · Start date · Fresh-trial end date (Properly Presented only) · Edits this month.** Calendar reminder at the end of each Properly Presented client's month 3 to offer the upgrade.

## 5. Upgrades and billing mechanics
- **New customers choosing Fresh:** "Simple Website + Fresh" link (£50 + £20/mo, £70 first payment).
- **Existing Live customers upgrading:** send the "Upgrade to Fresh" link (£20/mo), then **cancel their old £10 subscription** in Stripe so they are not billed twice. The confirmation page tells them you will confirm the switch.
- **Properly Presented after month 3:** bills at £10/mo throughout; the Fresh-level service is a perk, not a billing change. At month 3 offer the £20 upgrade via the upgrade link.

## 6. Failure modes to watch
- **Time creep:** if a Live client's average edit takes over 15 minutes, the price is wrong or the edits are not "everyday". Check the log.
- **Scope creep dressed as an edit:** "just add a booking page". Quote it.
- **Wrong client, wrong repo:** check the repo and domain before pushing.
- **Stale preview:** hard-refresh and check on a phone.

## 7. Automate later, not now
Stage 1 (now): manual, Claude-assisted, human reviews and sends every reply.
Stage 2 (when edits take real time, roughly 15+ clients): intake via the WhatsApp Business API, Claude drafts the change as a branch or pull request, a human approves, and the reply is a drafted message you send.
Do **not** let anything push to a live site or message a client without a human approving it. The sender-verification rule matters even more once it is automated.
