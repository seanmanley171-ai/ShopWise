# SHOPWISE — Full App (static, no build step)

Sean's third app. Shopping comparison: search once, compare the same product
across stores by **real total cost** (price + shipping + trip cost), stock,
and distance.

- Tagline: "Find the best deal. Not just the lowest price."
- Motto: "Shop smarter. Spend less. Waste nothing."
- Design: dark blue (`#0b1220` background, `#121d30` panels, green `#69e0a3`,
  blue `#8ebcff`, gold `#ffd27a`), mobile-first, bottom nav like UNTAPPED.

## Run it
Open `index.html` in a browser, or serve this folder with any static host
(e.g. GitHub Pages). No build step, no dependencies, no accounts.

## The five pieces (all in `index.html`)
1. **Compare** — search + ZIP (default 08232) + sort (Best overall value /
   Lowest total / Closest / Most stock). Total = price + shipping + trip
   (trip = distance × cost-per-mile, default $0.18/mi, round-trip estimate).
   Catalog: 36 products × 3–4 offers (140 sample offers) across Tech, Tools,
   Home, Kitchen, Gaming, Everyday; stores: Walmart, Target, Amazon,
   Best Buy, Home Depot, Lowe's, Dollar General, CVS.
2. **My List** — add offers from Compare; grouped by store; per-store
   subtotal counts the trip once per store; compares your split-store total
   vs the cheapest single store that carries everything, in dollars.
3. **Watch** — target price per product; HIT badge when the best sample
   total is at or under target.
4. **Savings** — log purchases via "Bought it" on a deal or by hand; totals:
   purchases, spent, saved (saved = highest sample total for the product −
   total paid, floored at $0). Real numbers from your entries only.
5. **Settings & Support** — ZIP, cost-per-mile slider/input, preferred-store
   filters, full data reset (with confirm), support contact
   seanmanley171@gmail.com, link to the privacy policy.

List, watches, purchases and settings persist in `localStorage` on the
device only. `privacy.html` says exactly that. `manifest.webmanifest` +
`sw.js` (cache name `shopwise-v1`, cache-first) make it an installable,
offline-capable PWA.

## ⚠️ HONESTY LAW — sample data only
**Every price, stock count, distance and shipping figure in this version is
SAMPLE / DEMO data.** It is not live, not scraped, and not verified against
any retailer. Every offer card in the UI is labeled "Sample" with a sample
timestamp, and the Compare tab carries a visible disclaimer.

**Never present this data as live retailer data.**

## Data layer = adapter seam
In `index.html`, the `CATALOG` / `STORE_META` block is the data layer and is
marked in comments as the **adapter seam**. A live version replaces that
block with retailer-specific adapter functions (one per retailer) returning
the same shape — `{ id, name, category, offers: [{ store, price, stock,
ship }] }` — plus a fetched-at timestamp per offer for inventory confidence.
UI, scoring, list, watch and savings code must not need to change.

No account, subscription, or payment rules exist for ShopWise yet — Sean has
not set them. Do not add any without his word.

## Files
- `index.html` — the whole app (HTML + CSS + JS)
- `privacy.html` — privacy policy (on-device data, no accounts, no tracking)
- `manifest.webmanifest` — PWA manifest (theme `#101827`, standalone)
- `sw.js` — service worker, cache-first, cache name `shopwise-v1`
- `icon.svg` — app icon
- `README.md` — this file
