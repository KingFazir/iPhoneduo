# Sponsor my iPhone Duo

Sell sticker spots on the back of the new iPhone Duo ($1,999, pre-orders
Oct 16, ships Oct 23). Companies bid for space — the bigger the spot, the
higher the price. If every spot sells at its starting bid, the phone pays
for itself.

The whole site is one file: **`index.html`**. No build step, no dependencies.

## The sticker playground

Visitors can drag sample stickers (or upload their own logo — it never
leaves their browser) onto an interactive, to-scale render of the Duo's
back panel:

- The phone tilts in 3D with the cursor, with a moving light sheen, in both
  real finishes (night sky / star white, toggle under the phone).
- Dropping a sticker on a dashed spot sizes it to that space and pops a
  "Bid on M-03" call-to-action; dropping elsewhere places it free-form.
- Stickers can't cover the camera plateau, and dragging one off the phone
  removes it.
- Want the real press photo instead of the CSS render? Save it cropped to
  the panel edges (e.g. `assets/duo-back.jpg`) and set
  `CONFIG.phoneImage: "assets/duo-back.jpg"` — spots and stickers overlay
  the photo. Mind the license on Apple newsroom images before publishing.

## How bids reach you

Bids are submitted in-page (no redirect) to the email in `CONFIG.email`
(bottom of `index.html`), through one of two free services:

- **Web3Forms (recommended)** — get a free access key at
  [web3forms.com](https://web3forms.com) (enter your email, the key arrives
  by mail, no account needed) and paste it into `CONFIG.web3formsKey`.
- **FormSubmit (fallback when no key is set)** — requires clicking a
  one-time activation email after the first submission, and the service
  has occasional outages.

If the delivery service is unreachable when someone bids, their email app
opens with the bid pre-filled and addressed to you — no bid is lost.

## Analytics

Cookieless analytics via [GoatCounter](https://goatcounter.com) (free,
no cookie banner needed): create an account, pick a site code, and put
it in `CONFIG.goatcounter` (e.g. `"sponsormyduo"` for a
`sponsormyduo.goatcounter.com` dashboard). Page views and a `bid:<spot>`
event per submitted bid are tracked. Leave the field empty to disable
analytics entirely.

## Managing the auction

Everything lives in the `CONFIG` object at the bottom of `index.html`:

- **Record a bid** — set `bid: 350` on that spot. The site updates the high
  bid, the "Outbid" button, the minimum next bid (+25%), and the phone-fund
  progress bar automatically.
- **Mark a spot won/paid** — set `sponsor: {name: "Acme", url: "https://acme.com"}`.
  The sponsor's name renders on the phone.
- **Change dates, goal, or minimum outbid %** — `closes`, `goal`, `minIncrease`.
- **Move/resize spots** — each spot has `x/y/w/h` as percentages of the
  84 × 118 mm panel (84.1 × 117.8 mm closed, per Apple's specs); the mm
  labels recompute automatically.

## Deploying

Any static host works. Two easy options:

### GitHub Pages (free, this repo)

1. Repo → **Settings → Pages** → Source: *Deploy from a branch* →
   Branch: `main`, folder `/ (root)` → Save.
2. Site goes live at `https://kingfazir.github.io/iPhoneduo/` in ~1 minute.

### Vercel or Netlify (free)

Import the repo at [vercel.com/new](https://vercel.com/new) or
[app.netlify.com](https://app.netlify.com) — no build command, output directory
is the repo root. Done.

## Custom domain: sponsormyiphoneduo.com

The repo's `CNAME` file already declares the domain. To finish:

1. At the domain registrar, add these DNS records:

   | Type  | Name | Value                  |
   |-------|------|------------------------|
   | A     | @    | `185.199.108.153`      |
   | A     | @    | `185.199.109.153`      |
   | A     | @    | `185.199.110.153`      |
   | A     | @    | `185.199.111.153`      |
   | CNAME | www  | `kingfazir.github.io`  |

2. Repo → Settings → Pages → Custom domain → enter
   `sponsormyiphoneduo.com` → Save, then tick **Enforce HTTPS** once the
   DNS check passes (can take a few minutes to a couple of hours).
