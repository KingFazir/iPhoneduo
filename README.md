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

The bid form posts to [FormSubmit](https://formsubmit.co) using the email set
in `CONFIG.email` (bottom of `index.html`).

> **One-time activation:** the first time anyone submits the form, FormSubmit
> emails you an activation link. Click it once and every bid after that lands
> straight in your inbox. Submit a test bid yourself after deploying to trigger
> the activation.

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

## Custom domain

1. Buy the domain at any registrar (Namecheap, Cloudflare, Porkbun —
   e.g. `sponsormyduo.com`).
2. **GitHub Pages:** Settings → Pages → Custom domain → enter it, then at your
   registrar add a `CNAME` record pointing `www` → `kingfazir.github.io`, and
   `A` records for the apex to GitHub Pages IPs (`185.199.108.153`,
   `.109.`, `.110.`, `.111.153`). Enable *Enforce HTTPS*.
   **Vercel/Netlify:** add the domain in the project's Domains settings and
   follow the two DNS records they show you.
3. HTTPS certificates are automatic on all three hosts.
