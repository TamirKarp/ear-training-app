# Outcome 2: Start a Practice Session on a Known Module

> Approved by Tamir on 2026-06-24. Four-trap quality review passed.
> Acid-test persona: Ruairidh. See `docs/personas/ruairidh.md`.

---

## Taxonomy (established during this outcome)

- **Module** — a large category: Intervals, Chords, Chord Sequences.
- **Element** — a specific exercise within a module: within Intervals → Major & Minor 2nds, Major & Minor 3rds, Melodic vs Harmonic, and so on.
- **Each element** has its own Practice and Test, and its own best Test score (%) and best time.
- **Scores live on the module page**, shown per element — never on the home screen.

(Open content-design question, parked: exactly how finely Intervals subdivides into elements, and whether ascending/descending/mixed and melodic/harmonic are separate elements or options within an element. Not blocking this outcome.)

---

## Field 1: Persona
**Ruairidh** — just handed the parent's phone in one of his short windows (car, waiting, after-dinner), about 85% of the time because a parent suggested it rather than because he asked. Mildly compliant rather than eager: he'll do it, but the app has seconds to convert "was told to" into "actually engaged" before his attention drifts to wondering what else is on the phone.

See: `docs/personas/ruairidh.md`

---

## Field 2: Trigger
A parent hands Ruairidh the phone for an ear-training session during one of his short windows — or, less often (~15%), Ruairidh asks for the phone to do it himself.

---

## Field 3: Walkthrough

### Happy path

1. The app is opened. The **profile picker** appears — one icon per family member, each showing its username. This happens on every launch, no exceptions, so no one ever lands in someone else's profile by default.

2. Ruairidh taps his icon. His **home screen** loads: his streak counter at the top, then the **Continue button** reading "Continue: [last element]", then the **list of modules** (Intervals, Chords, Chord Sequences). No scores appear on the home screen — home is about getting moving, not reviewing.

3. **Hot path — he taps Continue.**
   - If his last session ended cleanly, a fresh Practice session starts on that element. The first question loads and its audio plays — Outcome 1's trigger fires, and this outcome ends.
   - If his last session was interrupted mid-question, that exact question reloads as he left it: same question, prior wrong taps still red, replay button available. He picks up mid-thought, even an hour later.
   - This path is two taps from app-open to first audio, inside the 5–10 second budget.
   - (Continue's behaviour when his last activity was a *Test* is specified by the Test outcome, not here.)

4. **Browse path — he chooses something else.**
   - He taps a **module** (e.g. Intervals).
   - The **module page** opens: a row per **element** (Major & Minor 2nds, Major & Minor 3rds, Melodic/Harmonic…), each showing its best Test score (%) and best time — the visible proof-of-progress and the revisit hook. Each element offers a **Practice and a Test choice, inline**.
   - He taps **Practice** on an element. A fresh Practice session starts, the first question loads, and its audio plays. This outcome ends.

### Failure paths

**If the profiles fail to appear on launch:** a "try again" prompt. Nothing else — there is nothing else he can do, and nothing technical to explain.

**If Ruairidh's profile has no previous activity (brand-new profile):** no Continue button appears — there is nothing to continue. The module list is the entry point. (Choosing a username, and the first-ever video lesson for a never-seen element, belong to separate onboarding outcomes.)

**If an element's content fails to load after he taps Practice:** a brief "try again" message with a retry. He stays on the module page; nothing is lost.

**If a sibling taps Ruairidh's profile by mistake (or vice versa):** a profile-switch control on the home screen returns to the picker in one tap. Friction-light, per the persona's data-boundary notes.

**If the phone is taken between the profile tap and the first question:** nothing was started, nothing is lost. The next launch shows the picker as always.

---

## Field 4: Verification

1. On every launch, the profile picker appears with one icon per profile — no profile is auto-selected.

2. Tapping a profile icon loads that profile's home screen: streak at top, Continue button, module list.

3. The home screen shows no per-element scores — scores do not appear here.

4. Tapping Continue after a clean last session starts a fresh Practice session on the last element, and the first question's audio plays automatically.

5. Tapping Continue after an interrupted last session reloads that exact question with prior wrong taps still red.

6. On the Continue path, the time from app-open to first-question audio is within 5–10 seconds (two taps).

7. Tapping a module opens the module page, listing that module's elements.

8. Each element row shows its best Test score (%) and best time — or a clear "not attempted yet" state if none exists.

9. Each element offers both a Practice and a Test choice.

10. Tapping Practice on an element starts a fresh Practice session and the first question's audio plays.

11. If the profiles fail to load, a "try again" prompt appears — nothing else.

12. A brand-new profile with no history shows no Continue button; the module list is the entry point.

13. If an element's content fails to load after tapping Practice, a brief "try again" appears, Ruairidh stays on the module page, and nothing is lost.

14. A profile-switch control on the home screen returns to the picker in one tap.

15. If the phone is taken between the profile tap and the first question, the next launch shows the picker as normal with nothing lost.

**Notes for the QA agent:**
- Items 1–4, 7–14 are testable in a browser using Playwright.
- Item 5 (resume of an interrupted question) can only be verified end-to-end once the session-save outcome exists — see Dependencies. Until then, verify the clean-session branch of item 4.
- Item 6 is a timing check (app-open to first audio under the budget).

---

## Field 5: Contracts Exposed

**An active Practice session on a specific element:**
- A Practice session now exists, scoped to one element, with the first question selected and ready to play.

Consumed by:
- **Outcome 1 (Answer one Practice question)** — which takes over from the first question onward.

**The active profile:**
- The app now knows whose profile is in use. Every score, streak, and leaderboard position downstream is scoped to this profile.

Consumed by:
- Virtually every other outcome — Test, leaderboard, streak display, badges, dashboard.

**The navigation surfaces:**
- The profile picker, the home screen (streak + Continue + module list), and the module page (elements + best scores + Practice/Test fork) now exist and are reachable.

Consumed by:
- The Test outcome (the Test side of the fork), the leaderboard outcome, the streak-display outcome, and the badge/dashboard outcomes — all of which attach to these surfaces.

**Deliberately NOT produced here:**
- The best Test scores themselves — this outcome *displays* them; the Test outcome produces them.
- The persisted resume state — this outcome *consumes* it; the session-save outcome produces it.

---

## Field 6: Dependencies

- **Ruairidh's profile exists** — created by a profile-creation / onboarding outcome (separate). At minimum his profile must exist before he can tap it.
- **The module → element taxonomy and content exist** — the modules, their elements, and each element's question bank. From the content-loading outcome (separate).
- **Best Test scores per element** — produced by the Test outcome. If none exist yet, the module page shows a graceful "not attempted yet" state, so this outcome does not hard-depend on scores existing.
- **Persisted last-activity and interrupted-question state** — produced by the session-save outcome (separate). Needed for Continue's resume behaviour. If absent (clean exit, or first ever use), Continue simply starts fresh — so the clean-session branch can be built and verified before the session-save outcome exists.
- **Streak value** — produced by the streak outcome. Displayed on home; shows nothing/zero if absent.

The clean-session hot path and the browse path can be built and verified as soon as profiles and element content exist. The resume branch and the live streak display light up as their producing outcomes are implemented.

---

## Forward notes for the next outcome

- **Test-continue behaviour** — the Continue button is shared. Its behaviour when the last activity was a Test (and tests do not resume — interruption restarts them) must be specified by the Test outcome.
- **Module-page density** — each element row carries name + best % + best time + Practice + Test. On a 375px screen with 6+ elements this is dense; layout is Rachel's (design) concern, flagged here so it is not lost.
- **Profile creation / onboarding** — choosing a username (no password, per persona) and the first-ever-use flow are their own outcomes, depended on here but not specified here.

---

*Build outcomes for Ruairidh first. If this journey gets him from a handed-over phone to his first question inside 5–10 seconds on the hot path, the app has won the only battle that matters at session start: beating YouTube to his attention.*
