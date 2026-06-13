# Your marketing budget is bleeding. Fix it.
### A bespoke ABM demo microsite — Prepared for Airwallex · Powered by AppsFlyer

A single-page, mobile-first demo microsite built for a university marketing project
(Reichman University, Digital Marketing). It's an **Account-Based Marketing (ABM)** page
built for **one** target account — **Airwallex** — and is the destination of a QR code on a
personalized postcard mailed to Airwallex leadership.

The page continues the postcard ad (*"Your marketing budget is bleeding. Fix it."*), then
uses a mock **AppsFlyer Creative Optimization** dashboard to "analyze" Airwallex's real
flagship campaign — the Arsenal **"Who Are Ya?"** film — and show which few cuts to scale
and which are quietly bleeding budget.

> **It wears Airwallex's brand** (Electric Violet accent) as the deliberate ABM statement —
> *"we built this for you."* **AppsFlyer is the sender**, present via its wordmark and product
> voice, not as the colour scheme.

---

## What's in the box

```
appsflyer-airwallex/
├── index.html      ← the entire site: inline CSS + JS, one Google Fonts link, zero build
└── README.md       ← this file
```

`index.html` is **fully self-contained**. No backend, no build step, no `localStorage` — all
state lives in JS memory. The only external dependency is Google Fonts (Inter + JetBrains Mono).
The card thumbnails are **brand-safe stock photos (Pexels licence), compressed and inlined as
base64 data-URIs** inside the script — generic football / pub / broadcast scenes with no real
players, club crests or sponsor logos, so the file still travels as a single document (~310 KB).
To swap them, replace the `IMG` data-URIs and the per-card `IMG_MAP` near the top of the script.

---

## Preview locally

Because the page references Google Fonts over the network, just open it or serve it — either works:

**Option A — double-click.** Open `index.html` in any modern browser.

**Option B — serve it (recommended; closer to production):**
```bash
cd appsflyer-airwallex
python3 -m http.server 4178
# then visit http://localhost:4178/index.html
```
or, if you prefer Node:
```bash
npx serve .
```

Test it at **~375px wide first** (most visitors scan the QR on a phone), then widen.

---

## Get a public URL in under a minute (two zero-config options)

You need a real https URL to point the QR code at. Both of these are free and need no build.

### 1. Netlify Drop — the fastest
1. Go to **https://app.netlify.com/drop**
2. **Drag the `appsflyer-airwallex` folder** onto the page.
3. Netlify gives you a live URL instantly, e.g. `https://airwallex-fixit.netlify.app`.
   (Optional: create a free account to rename the site / keep it.)

### 2. Vercel — also zero-config
**Drag-and-drop:** go to **https://vercel.com/new**, import or drop the folder, click **Deploy**.

**Or via CLI:**
```bash
npm i -g vercel
cd appsflyer-airwallex
vercel        # answer the prompts; accept defaults — it's a static site
vercel --prod # promote to the production URL
```
Either way you get a URL like `https://airwallex-fixit.vercel.app`.

> No framework settings needed for either — it's a static `index.html`, so "no build command /
> output directory = the folder" is correct.

---

## Build the per-executive URLs (the ABM personalization)

The page reads three URL query params. **With no params it defaults to Airwallex, addressed to
the company** — Airwallex branding and the *Who Are Ya?* content are the baseline, not a fallback.

| Param  | Values                         | Effect                                                                 |
|--------|--------------------------------|------------------------------------------------------------------------|
| `name` | any name, e.g. `Jack`, `Lucy`  | Greets the individual: *"Jack — your marketing budget is bleeding."*   |
| `role` | `ceo` · `cmo` · `team`         | Selects the **messaging angle** (not a literal job title) — see below. |
| `verb` | `bleeding` · `leaking`         | Swaps the headline word to match the printed postcard. Default `bleeding`. |

**`role` angles**
- `ceo` → global growth & protecting margin while spending big on brand.
- `cmo` → proving ROAS on a flagship brand spend; AI **augments** the team.
- `team` → less manual cut-by-cut testing; faster wins.

**The two postcards** (replace `YOUR-URL` with your deployed domain):

```
Jack Zhang  (Co-Founder & CEO, postcard says "bleeding"):
  https://YOUR-URL/?name=Jack&role=ceo&verb=bleeding

Lucy Liu  (Co-Founder / President, postcard says "leaking"):
  https://YOUR-URL/?name=Lucy&role=cmo&verb=leaking
```

> Tip: URL-encode names with spaces (`Jack%20Zhang`). A jump straight to the form is
> `https://YOUR-URL/#cta`.

---

## Make the QR code (for slide 7)

1. Deploy and copy your **per-executive URL** (above).
2. Paste it into any QR generator — e.g. **https://www.qr-code-generator.com** or
   **https://qrcode.tec-it.com** — and download a high-res **SVG/PNG**.
3. Drop the QR onto the postcard mockup / slide 7. Generate **one QR per executive** so each
   scan lands on that person's personalized page.
4. **Test the QR with a real phone** before printing — scan it, confirm the right name and verb
   appear, and that the slider/dashboard/form all work on the phone.

---

## Re-skinning for another account (or the generic booth)

Everything account-specific lives in **clearly labeled config blocks at the top of the
`<script>`** in `index.html`:

- **`:root` CSS variables** (top of `<style>`) — the brand palette and type tokens.
- **`CONFIG`** (top of `<script>`) — account name, default monthly spend + meter range, the
  illustrative `wasteFraction`, the cited 2% / 68% stat, the channel spend data, the **campaign
  cut cards**, and all personalization copy (role lines, sublines).

To rebrand: swap the `:root` colours and the `CONFIG.account` / `CONFIG.cuts` / `CONFIG.copy`
values. Nothing else needs to change.

**Logo slots:** the page renders **text wordmarks** for "AppsFlyer" and "Airwallex". Each has a
clearly commented `>>> LOGO SLOT <<<` in the markup where you can paste an official SVG/PNG later.

---

## Honesty & rights (please keep these intact)

- This is a **student class demo** — a concept piece, **not** an official Airwallex or AppsFlyer
  product, and not affiliated with or endorsed by either company, Arsenal FC, or anyone named in
  the *Who Are Ya?* campaign.
- All spend figures, the bleeding meter, and the dashboard scores are **illustrative estimates,
  simulated for demonstration** — they are not Airwallex's real performance data.
- The **only** hard statistic stated as fact is **2% of creative variations command 68% of ad
  budget**, attributed to **AppsFlyer, *State of Creative Optimization***.
- Card thumbnails are **generic licensed stock photos (Pexels)** used only to set a mood — they
  are **not** stills from the *Who Are Ya?* film and contain **no real player/celebrity
  likenesses, club crests, or sponsor logos**. The cut names are illustrative labels. No brand
  assets are hotlinked or scraped.

---

## Accessibility & browser support

- Mobile-first, responsive from ~375px up.
- Semantic HTML, real `<label>`s on every input, visible keyboard focus, `aria-live` on the
  meter readout and form result.
- Win/loss is never signalled by colour alone — every state carries an icon **and** a text label.
- Respects `prefers-reduced-motion` (count-ups and scroll reveals collapse to their end state).
- Works in any modern evergreen browser (Chrome, Safari, Firefox, Edge).
