# getPresented. — getpresented.co.uk

Static site for the UK brand, hosted on GitHub Pages. Plain HTML/CSS/JS, no build step. Push to `main` and it's live in about 2 minutes.

**The working codex is [`CLAUDE.md`](CLAUDE.md)**: products and pricing, Stripe links, repo map, design tokens, tracking rules, open items and decisions. Start there. Client edit requests follow [`docs/edit-workflow.md`](docs/edit-workflow.md).

## Quick edit
Each page is a single self-contained HTML file. Find the visible text, edit it, commit, push. If you change a price or add a product, follow the rules in `CLAUDE.md` §8 (confirmation page, Purchase value, `llms.txt`, meta descriptions).

## Don't touch without care
The cookie-consent and Meta Pixel block at the top of every page, WhatsApp `onclick` Lead handlers, and Stripe payment links.
