# CLAUDE.md template for a client's site repo

Copy this into the root of each client repo as `CLAUDE.md` and fill in the blanks. Its job is to let Claude make a safe, small edit from a WhatsApp message without re-learning the site each time. Keep it short.
**Client repos are public** (free GitHub Pages, per the build SOP), so this file must contain nothing private: no phone numbers or emails of the client, no payment details, no internal pricing or plan strategy. Keep those in your private client list. Also add this to the client repo so the file isn't published on the site:

`_config.yml`
```yaml
exclude:
  - CLAUDE.md
  - EDITS.md
```

---

```markdown
# <Client business name>: site notes for Claude

## Who and what
- Business: <name>, <what they do>, <where>
- Domain: <domain>   Repo: <repo>   Hosting: GitHub Pages (static, no build step)
- Plan: <Live | Fresh | Properly Presented>
- Client contact details and the WhatsApp number on file: kept in Glancy's private client list, not here
- Owner of the work: getPresented. (Glancy)

## How to make a change
1. Read the edit brief. If anything is unclear, stop and ask one question.
2. Change only what the brief says. No refactors, no drive-by tidying.
3. Show the diff and summarise it in plain English.
4. Do not push. Glancy reviews and pushes.

## Rules
- Never change: phone numbers, email addresses, payment/bank details, outbound links, form endpoints or DNS files, unless the brief explicitly says so and Glancy has confirmed it with the client.
- Prices, hours and opening times: use the client's exact words. Never infer.
- Photos: compressed, descriptive filenames, saved in `assets/images/`, real alt text.
- Keep the client's existing fonts, colours and layout. Do not restyle.
- Language: British English unless the site is Spanish.

## Site map
| Page | File | Notes |
|---|---|---|
| Home | `index.html` | <hero, services, hours section ids> |
| ... | ... | ... |

## Design tokens
<colours, fonts, from the site's :root>

## Contact form
<FormSubmit or other, destination alias, do not change>

## Things the client has asked for before
<short list, e.g. "always show prices inc. VAT">

## Edit log
See `EDITS.md`.
```
