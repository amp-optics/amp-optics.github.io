# AMP Optics website

Static replacement for the Squarespace site at https://www.amp-optics.com/ — plain HTML/CSS, no build step, no CMS, free to host.

## Structure

| Path | Page |
|---|---|
| `index.html` | Welcome (homepage) |
| `about-us/` | About Us |
| `services/` | Services |
| `publications/` | Publications |
| `contact-us/` | Contact (form) |
| `privacy/` | Privacy policy |
| `s/` | Publication files (same URLs as on Squarespace) |
| `assets/` | Stylesheet, logo, hero image, favicon |

The two brochure PDFs were removed: the back brochure carried a Contact Us block with an
email address and phone number that the site deliberately omits. Originals are kept at
`C:\Users\amphe\amp-optics-brochures-backup\`. To re-add a brochure, drop a contact-free
PDF into `s/` and restore the download line at the end of `services/index.html`.

URL paths match the old Squarespace site exactly, so existing links and search results keep working.

## Editing content

Each page is a single HTML file — edit the text between the tags and push. To add a publication, copy an existing `<li>` block in `publications/index.html` and edit it.

## Contact form (one-time setup)

The form posts to [Web3Forms](https://web3forms.com) (free). To activate it:

1. Go to https://web3forms.com and create an access key for the business inbox (no account needed — the key arrives by email).
2. In `contact-us/index.html`, replace `YOUR_ACCESS_KEY_HERE` with that key.
3. Submit a test message and confirm it arrives.

The "enter the word 'Light'" spam question is enforced in the page's JavaScript before anything is sent.

## Deploying (GitHub Pages)

Repo: https://github.com/amp-optics/Website

1. **The repo must be public** for GitHub Pages on a free account. Pages on a private repo
   requires a paid GitHub plan.
2. Repo → Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. The site appears at `https://amp-optics.github.io/Website/` — verify everything there first.
4. Repo → Settings → Pages → Custom domain: enter `www.amp-optics.com`, and check "Enforce HTTPS" once it validates.

A `CNAME` file with `www.amp-optics.com` is included so the custom domain persists across pushes.

## DNS cutover (at the registrar, dns1–5.name-services.com panel)

**Change only these records. Do not touch MX or TXT records — that's the Google Workspace email.**

| Record | Current (Squarespace) | New (GitHub Pages) |
|---|---|---|
| `www` CNAME | `ext-cust.squarespace.com` | `amp-optics.github.io` |
| apex `@` A ×4 | 198.185.159.144/145, 198.49.23.144/145 | 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153 |

TTL is 30 minutes, so the switch completes quickly. The Squarespace site keeps serving until DNS flips — zero downtime.

## After cutover

1. Verify `https://www.amp-optics.com` and `https://amp-optics.com` load with valid HTTPS.
2. Send a test message through the contact form.
3. Send/receive a test email to confirm Google Workspace is untouched.
4. Cancel the Squarespace subscription (Settings → Billing). Don't cancel before the new site is confirmed live.
