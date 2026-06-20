# YesCoach — The First-Session Wow

*Created: 2026-05-26 | Purpose: define the activation moment and align marketing to deliver it*

This doc exists to fix the come-and-go problem (users download, don't stick). It names the
first-session wow precisely and corrects the hero marketing assets to point at it. Builds on
[knowledge-context.md](./knowledge-context.md) and [marketing-strategy.md](./marketing-strategy.md);
supersedes the manual-flow demo in [video-overlay-script.md](./video-overlay-script.md) for
*acquisition/activation* purposes (that script's pro-flow cut stays useful for power users).

---

## 1. The model

**The newcomer path is NOT manual building.** Tap-a-muscle → configure → add is the **pro**
flow — impressive, but too much lift for a first-timer. The newcomer wants to start fast:

> **ready plan / template → train → log → SUBMIT → wow**

- **On-ramp (live now): templates / ready plans.** Carry a newcomer to a logged session
  without pro-level effort.
- **On-ramp (coming): smart generation.** The hot-sell upgrade. Build-in-public it now; make
  it the hero of the *next* video once it ships.
- **The wow is post-submit**, and it's data-honest in session one because it shows *this*
  session, not a week of history.

## 2. The wow, exactly (updated 2026-05-30 — prototype landed)

The "Session Complete" summary modal was removed — submit jumps **straight to the Day View**.
Current flow:
1. Tap submit → confirm toast **"Complete workout? (N sets)"** → **Submit**.
2. Jump directly to the **Day View**. The body-map heatmap **animates: glows brightly on the
   muscles you just worked, then recedes to their true heat-map colors.** That glow→settle
   cycle *is* the wow — honest in session one (it's *this* session's data).
3. If this is the qualifying workout, the beta unlock fires first (premium-unlock celebration),
   then returns to the Day View — a bonus reward beat tied to the 3-workouts offer.

**Both product blockers resolved.** Animation trigger is wired on submit (prototype 2026-05-30),
and **"Choose Template"** is the first action in the Plan view — templates importable into the
plan immediately. The templates themselves are still candidates for design polish (non-blocking
— they work today). Video is unblocked.

## 3. The leak this fixes

Today a newcomer can hit the pro-level manual build *before* ever reaching the post-submit
payoff — so they bounce before logging anything, and never see the wow. Templates carry them
across that gap. Marketing's job: promise the template→wow path (not the pro path), set the
expectation that **the payoff lands after you log a session**, and frame the body map as a
neutral mirror, not a scorecard (per the wife-feedback insight in knowledge-context.md).

---

## 4. Hero video — "Your first session" (45–60s, the activation asset)

Record one continuous flow. Text overlays in edit. Data-honest: every screen below is real.

| # | What you do | Text overlay |
|---|-------------|--------------|
| 1 | Open app | **"New here? Start in seconds."** |
| 2 | Pick a ready plan / template | **"Pick a ready plan."** |
| 3 | Plan loads — exercises ready | **"Your session's built. No setup."** |
| 4 | Log sets — weight, reps, effort (RIR) | **"Train. Log it. Weight, reps, effort."** |
| 5 | Tap submit → "Complete workout?" → Submit | **"Done? Submit."** |
| 6 | Day View opens — body-map heatmap **glows** on the muscles you just trained | **"Instantly — see exactly what you worked."** ← THE WOW |
| 7 | Glow **recedes** to true heat-map colors (the real activation reading) | (hold the overlay from beat 6 — let the animation breathe) |
| 8 | Linger on the settled body map | **"Not a list. Your body."** |
| 9 | End card | **"YesCoach — free on Android · yescoach.fit"** |

**Pacing:** hold beats 6–8 longer than the rest — the glow→recede cycle IS the wow; don't rush
it. Each overlay ≥ 1.5–2s. No voiceover required; overlays carry it. Music: low-fi, quiet.

**Why this beats the existing demo for activation:** the on-file script opens with "tap a
muscle, configure, add" — the pro flow. A confused first-timer never gets to the payoff. This
cut shows the *easy* path and ends on the lit body map, so the promise = the real first session.

### Short cut (≤30s, for X / Reels / Shorts / TikTok)
Compress to: pick a plan → log → submit → **body lights up.** Hook text:
*"Most apps just log your workout. Watch what this one does when you hit submit."*

---

## 5. Promise alignment (so expectation = reality)

Everywhere a newcomer forms expectations — store listing, website, video thumbnail, X/Reddit
posts — lead with the template→wow path, not the pro build:

- **Do say:** *"Pick a ready plan, train, and see exactly which muscles you worked."*
- **Don't lead with:** *"Tap any muscle and build your own workout"* (true, but it's the pro
  path — it sets up the friction that makes people bounce).
- **Frame the body map as a mirror:** *"Here's your session"* — never *"here's what you
  neglected."*

## 6. Smart generation (the coming hot sell)

Templates are the on-ramp today; smart generation is the upgrade that makes the easy path
*personal*. Tease it in build-in-public now ("building smart workout generation — here's the
hard part"), and when it ships, it becomes the hero of the next first-session video, replacing
"pick a ready plan" with "generate my session."

---

## 7. Open items

- ~~Product/dev — restore the body-map animation on submit.~~ ✅ **Resolved 2026-05-30** (glow→recede prototype).
- ~~Product/dev — make the template on-ramp the default first action.~~ ✅ **Resolved 2026-05-30** ("Choose Template" is first in the Plan view).
- Confirm the exact in-app label for overlay #2 (likely **"Choose Template"** — confirm wording).
- Decide where the hero video lives on yescoach.fit (above the fold) and in the Play listing.
- *Non-blocking future polish:* refine the templates themselves (selection, structure, naming).
  The current set works for the demo and acquisition; a better-curated library will strengthen
  the on-ramp for retained users. Doesn't gate the video.

---

## 8. Come-back DM — for the 3 current organic users

These three tried the *old* flow before the wow fix. Don't promise the lit-up body map until
product wires it. Two messages, sequenced.

### Send NOW — feedback-first
> "Hey [name] — solo builder behind YesCoach. Noticed you tried it and didn't come back.
> Totally fair — the first session doesn't yet explain itself fast enough, and I'm fixing that
> this week.
>
> If you've got 60 seconds: what was the first thing that confused or stopped you? Blunt is
> better than polite — I'd rather hear it than guess."

### Send AFTER the animation + template-default fixes ship — come-back
> "Hey [name] — quick follow-up. Shipped the change I mentioned: pick a ready plan, train, hit
> submit, and the body map lights up with the muscles you actually worked. That's the moment
> that wasn't landing before.
>
> Worth one more shot? Honest feedback on what works and what doesn't is the whole loop right
> now — that's the trade."

The whole app is free under Model A — there's no premium incentive to dangle. For new downloads
going forward, use the "DM Template (New Downloads)" in
[execution-plan.md](./execution-plan.md).
