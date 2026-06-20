# YesCoach — Netlify → Cloudflare Pages Migration Runbook

*Created: 2026-06-08 | Scope: marketing-side migration of yescoach.fit.*

**Target stack:** Cloudflare Pages (hosting) + Google Apps Script → Google Sheets (waitlist) + Namecheap (registrar, unchanged). Reference for the waitlist endpoint: `docs/setup/email-collection-landing-page.md` Option 1 in the YesCoachReact repo.

**Goal:** zero data loss on the waitlist, zero analytics gap, zero broken share-links, no redirect-warning carryover.

---

## Pre-flight — capture state before touching anything

- [ ] **Export Netlify Forms data → CSV.** Netlify dashboard → Forms → export. Store in Drive + local. Irreplaceable artifact.
- [ ] **Identify the marketing-site source repo on GitHub.** Cloudflare Pages deploys from it. *(If the site doesn't already live in its own repo, decide now: split it out, or deploy from a subfolder of an existing one.)*
- [ ] **Snapshot Google Analytics baseline** — last-30-day sessions, top sources, conversion events. Used to verify continuity post-move.
- [ ] **PageSpeed Insights baseline** for `yescoach.fit` (mobile + desktop). Goal post-move: ≥ baseline.
- [ ] **Save current OG meta tags.** View source → copy `og:title`, `og:description`, `og:image`. If the image URL is hosted on Netlify, re-host it before cutover.
- [ ] **Screenshot current Namecheap DNS records** for yescoach.fit. Rollback safety net.
- [ ] Confirm the GA measurement ID is in build-time env vars (or hardcoded) and survives the move.

## 1 — New waitlist endpoint (Google Apps Script → Sheets, ~5 min)

Per Option 1 in `docs/setup/email-collection-landing-page.md`. Zero new vendors.

- [ ] Create Google Sheet **"YesCoach Email List"** with headers: `timestamp`, `email`, `source`, `userAgent`.
- [ ] Paste the Apps Script `doPost` from the setup doc. Deploy as **Web app · execute as Me · anyone**.
- [ ] Copy the deployment **Web App URL**.
- [ ] Replace the Netlify Forms handler in the site code with a POST to that URL (the `EmailCollectionForm` pattern in the setup doc).
- [ ] **Import the Netlify CSV** into the sheet so the new sheet holds the full historical waitlist.

## 2 — Deploy to Cloudflare Pages (preview first)

- [ ] Create Cloudflare account (free, no credit card).
- [ ] CF Dashboard → Pages → **Connect to Git** → pick the marketing-site repo + branch.
- [ ] Set build command + output dir matching the site framework.
- [ ] First deploy → verify on the `*.pages.dev` URL: layout, images, GA fires, form submits, Play Store link clean.
- [ ] Fix anything broken on `*.pages.dev` **before** attaching the custom domain.

## 3 — DNS pre-cutover (Namecheap)

- [ ] **At least 24h before cutover:** lower TTL on yescoach.fit's DNS records to **300s (5 min)** in Namecheap. Limits propagation pain.

## 4 — Cutover (attach the custom domain)

- [ ] In CF Pages, add `yescoach.fit` and `www.yescoach.fit` as custom domains. CF will surface the exact records needed.
- [ ] In Namecheap DNS — pick one:
  - **Recommended:** **delegate nameservers to Cloudflare** (full DNS move — gets DDoS + CDN wins). Namecheap → Domain → Nameservers → Custom DNS → CF nameservers shown in your CF dashboard.
  - **Lighter:** keep Namecheap DNS, set A/AAAA/CNAME records per CF's instructions.
- [ ] Wait for SSL provisioning (CF auto-issues, usually <15 min — can take a few hours).
- [ ] Verify `https://yescoach.fit` serves from Cloudflare. `curl -I https://yescoach.fit` should show a `cf-ray` header.

## 5 — Post-cutover QA (each must pass before moving on)

- [ ] **Site loads** on yescoach.fit — incognito + mobile + desktop.
- [ ] **SSL/HTTPS clean** — no mixed-content warnings, lock icon green.
- [ ] **All routes + images** load. Above-the-fold, screenshots, Play link area.
- [ ] **OG meta tags intact** — paste a yescoach.fit URL into the X / LinkedIn / Facebook share debuggers; previews render correctly. Re-host any OG image that was on Netlify.
- [ ] **Google Analytics fires** — open GA real-time, load the site, see yourself appear.
- [ ] **Waitlist form** — submit a test email; verify the new row appears in the Google Sheet. Test duplicate-rejection.
- [ ] **Play Store link is a direct link** — `play.google.com/store/apps/details?id=...`, no intermediate redirect. Test mobile (Android) + desktop. **The "site may redirect you" warning must not appear** — this is the funnel-leak fix.
- [ ] **PageSpeed Insights ≥ baseline** (mobile + desktop).
- [ ] **sitemap.xml + robots.txt** served correctly.
- [ ] **Search-discoverability** — yescoach.fit still shows correctly in Google (cached preview re-crawls within a few days; no canonical mismatch).

## 6 — Bonus while you're in the code: hero copy swap

You're already in the codebase — swap the hero to the activation-aligned copy in
[first-session-promise-copy.md](./first-session-promise-copy.md) §2 ("See exactly what you worked"
headline + sub + CTAs). Two upgrades, one round of work.

## 7 — Decommission Netlify (after 48h clean)

- [ ] After 48h of stable traffic on CF, delete the Netlify site.
- [ ] **Keep the Netlify Forms CSV export filed safely** — final backup.
- [ ] Update internal docs that reference Netlify (knowledge-context.md `Current Marketing State`, CLAUDE.md if applicable).

## 8 — Update marketing memory

- [ ] Update `clients/yescoach/knowledge-context.md` → "Current Marketing State" → host = **Cloudflare Pages**, waitlist = **Google Apps Script → Sheets**.

---

## Risk + rollback

| Step | Risk | Mitigation |
|------|------|-----------|
| 4 — DNS cutover | Site briefly serves stale / broken | TTL lowered ahead in step 3; revert Namecheap to screenshot if needed; Netlify still live until decommissioned |
| Waitlist | Form data loss in cutover | CSV export in pre-flight; worst case re-import |
| Analytics | Gap in tracking | Same GA property ID kept; gap ≤ propagation window |
| Social shares | OG previews break | OG tags moved 1:1; OG image re-hosted if needed |

---

**Owners:** dev/founder runs steps 1–4 (CF + DNS + form wiring + code changes). Marketing follows
up step 5 visibility QA (OG previews, GA continuity, redirect-warning verification, hero copy
update) and steps 7–8 (decommission + doc updates) once cutover lands.
