# Life Charge Chiropractic — $49 New Patient Special Landing Page

Conversion landing page for ad traffic (Google, Facebook/Instagram, etc.) driving the
**$49 New Patient Special** offer for Life Charge Chiropractic in Gallatin, TN.

A static site — no build step. Deployable as-is to GitHub Pages, Netlify, Vercel,
Cloudflare Pages, or any static host.

## Pages

- **`index.html`** — the $49 offer landing page (conversion-focused, no outbound links)
- **`learn.html`** — interactive patient education page ("How Whole-System Chiropractic
  Works"): clickable spine explorer, symptom-vs-root-cause toggle, real Visit 0 → Visit 10
  thermal scan comparison, three-phase care journey, and a 60-second self-check quiz that
  funnels into the $49 offer. Use it for organic social, email follow-ups, and warming up
  leads who aren't ready to book yet. The landing page intentionally does **not** link to
  it, so paid ad traffic stays focused on the form.

## Page structure

1. **Minimal sticky nav** — logo, phone, "Claim $49 Special" button (no distracting links)
2. **Hero** — $49 offer badge, what's-included checklist, inline lead capture form with phone fallback
3. **Trust bar** — same-week appointments, no referral, bilingual, address
4. **What You Get** — 6-card grid breaking down the visit, ending in a dark $49 offer card
5. **Reviews** — 3 patient reviews + 5.0 Google badge
6. **Meet Dr. Palmer** — photo, bio, credentials grid
7. **How It Works** — 3 steps from pain to a plan
8. **FAQ** — 6 common questions
9. **Final CTA** + **sticky bottom offer bar** that appears after scrolling past the hero

## Lead funnel wiring

### Form destination
The form currently shows the success state without sending data anywhere. To receive
leads, set `FORM_ENDPOINT` at the top of the script in `index.html` to a form backend
URL (Formspree, Basin, Make/Zapier webhook, or your booking system's lead API):

```js
var FORM_ENDPOINT = 'https://formspree.io/f/XXXXXXXX';
```

Submissions are POSTed as form data: `name`, `phone`, `email`, `concern`, plus
attribution fields (below).

### Ad attribution
UTM parameters and click IDs (`utm_source`, `utm_medium`, `utm_campaign`, `utm_term`,
`utm_content`, `gclid`, `fbclid`) are captured from the landing URL into hidden form
fields automatically, so every lead carries its ad source. Point each ad at a tagged
URL, e.g.:

```
https://yourdomain.com/?utm_source=facebook&utm_medium=cpc&utm_campaign=49-special
```

### Conversion tracking
On successful submit, the page fires `gtag('event', 'generate_lead', …)` and
`fbq('track', 'Lead', …)` **if** the Google tag / Meta Pixel are installed. Paste your
tag snippets into `<head>` to activate them.

### Canonical URL
Update the `<link rel="canonical">` and `og:image` URLs in `<head>` once the final
domain is known.

## Design source

Implemented from the Claude Design handoff bundle ("Life Charge Chiropractic Design
System" — `New Patient Special.html`), using the official brand tokens: Life Charge
Red `#ED3237`, Yellow `#FFCC29`, Deep Charcoal `#2D2D2F`, Warm Cream `#FFF7E8`, the
red→orange→yellow brand gradient, Montserrat (local variable font) and Lora (Google
Fonts) typography. Mobile-responsive styles, SEO/OG metadata, LocalBusiness JSON-LD,
and the attribution/endpoint wiring above were added on top of the prototype.
