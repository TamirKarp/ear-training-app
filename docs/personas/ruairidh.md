# Ruairidh — 10-year-old beginner guitarist
> Persona created with ODD Studio. Acid-test persona: YES.

---

## Identity
Ruairidh is ten years old, in Year 6 at a small state primary school in the UK. He is a dirty-knees outdoor kid — football, scootering, the kinds of sports that scuff trousers. Six months ago he chose to start learning the guitar himself. He has private lessons once a week and is at the very beginning of his journey: a handful of chord shapes, no theory, no ability to read music, barely any sense of the note names on the fretboard.

He loves the *idea* of being a guitar player more than the *work* of becoming one. Left to his own devices he is not self-motivated to grind out practice. He needs the world around him to give him reasons to pick the guitar — or the phone — up.

---

## Reality
Ruairidh does not have his own phone. When he uses this app, it is a parent's phone, handed over for a specific window. The parent is often the one initiating the session — "do that ear thing instead of YouTube".

There are three recurring windows:
1. **Short car journeys** — driven somewhere, two to ten minutes of dead time.
2. **Waiting moments** — for a sibling at an activity, or a parent finishing something.
3. **A few minutes after dinner** — sitting at the cleared table while the kitchen winds down.

Sessions are 2–5 minutes, once or twice a day. He plays the audio through the phone's built-in speaker the vast majority of the time — headphones happen only very occasionally. A parent is in earshot and aware he is on it, but does *not* operate the app — at ten he is more fluent with the phone than the parent is. The parent's role is access control, not co-operation.

The session does not feel to him like "practice". That is part of why he engages.

**Implied design constraints:**
- Audio must work on phone speaker — cannot assume headphone fidelity.
- App must be openable and meaningful inside 2 minutes.
- "Pick up where you left off" must be obvious to *him*, with zero parent involvement.

---

## Psychology
- **Attention span:** roughly 5 minutes baseline on something he likes. Gamification (especially a leaderboard) is expected to extend that.
- **Competitiveness:** distinctly outward-facing. He asks "are other kids doing this? how are other people getting on?" A leaderboard will land.
- **Response to praise:** earned praise lands as a small dopamine hit. Hollow praise — "well done!" after a wrong answer — would patronise and erode trust. The household model is *supportive-but-honest*: "good effort, here's what you did well" after a miss.
- **Self-perception:** overconfident. "The joy of ignorance in his lack of ability." He sits in unconscious incompetence — does not yet know how much he does not know. He will not be embarrassed by mistakes (good — encourages engagement) but may rush from Practice into Test mode prematurely, thinking he has it. Test mode must give him honest feedback without crushing the confidence that is keeping him on the app at all.

---

## Trigger
Approximately **85% parent-initiated, 15% self-initiated**. Tamir explicitly frames this ratio as the design problem the gamification is meant to shift — every incentive built into the app exists to move the needle toward self-initiation.

Trigger sources, ordered by dependability:
1. **Parent hands the phone over.** Most reliable, but it is the trigger we are trying to *need less*.
2. **Guitar lesson.** Touching ear training in a lesson reminds him this is a skill that needs work. Because ear training is less tangible than playing the instrument, it is easy to forget — the lesson reactivates the thought "I should do that on the app".
3. **Score chase.** Beating a previous percentage *and* beating a previous time, both axes.
4. **Leaderboard pull.** Seeing other kids ahead of him spurs him on.
5. **Self-prompted "I want to do my ear training".** Rarest. The goal state.

**Rhythm.** Longer car journeys → more frequent sessions. **School holidays → less inclined to use it** — parents push educational activities less when not in term, and he follows suit. **Breaks in lesson schedule** (teacher away, term break) → engagement also drops.

**Critical implication.** The danger zone is school-holiday + lesson-break overlap, when both external scaffolds go quiet at the same time. The internal-pull mechanisms (leaderboard, score chase) must be strong enough to bridge that gap, or the app dies during long holidays.

---

## History
**Prior music theory: near-zero.** Knows a handful of chord shapes. Knows the words "major" and "minor" exist as chord categories but does not know what makes a chord major or minor. Cannot read music. Barely knows the note names on the fretboard.

**Prior ear training exposure: none.** The only prior reference frame for ear discrimination is a couple of lessons where his teacher used "major sounds happy, minor sounds sad" to anchor the distinction. That emotional/affective framing is the only existing pedagogical bridge.

**Mid-session interruption behaviour.** Tests do NOT resume — if the parent takes the phone back during a test, next time he starts that test from scratch. No pause/resume infrastructure needed. Practice sessions are interrupt-tolerant by design — each question is independent and there is no score continuity to preserve.

**Cross-session persistence model:**
- Per-module progress (which modules completed, how far through each)
- Per-test best percentage AND best time
- Per-test leaderboard ranking
- Duolingo-style streak counter — consecutive days of use, kept alive by *any* session including a brief practice

**Identity model.** Netflix-style. One device-level login (parent's), multiple profiles on it, profile picker on launch. Ruairidh taps his icon and his streak/scores/leaderboard rank load instantly. No password for him to remember. The same install accommodates siblings with their own profiles and separated progress.

---

## Success
Success operates at five scales for Ruairidh.

**1. Single question.**
Multiple-choice buttons turn green (correct) or red (wrong). No celebration animation at the question level. In Practice mode only, wrong answers also play back what the wrong option *would* have sounded like, so he hears the difference between his guess and the correct answer — turning misses into comparative listening moments.

**2. Test completion.**
End screen shows percentage and time plus a comparison to his previous attempt. On exit from the test, a separate screen shows his position on the leaderboard and his movement. This is the celebration peak — the rest of the app stays restrained so this lands.

**3. Daily streak.**
A single activity (Practice OR Test) advances the streak by one day, Duolingo-style. Streak milestones are celebrated with pre-recorded virtuosic guitar licks of escalating absurdity — standard daily lick, more intense at one week, ridiculous at a fortnight, full Van Halen-esque two-handed tapping at a month.

**4. Module completion.**
A module is "mastered" when its content can be identified — but this is explicitly **not a terminal state.** The app keeps surfacing levers to revisit completed modules: improve time, push toward 100%. The guiding analogy: *you never complete playing an instrument, you can always get better — same here.* The explicit anti-goal is the user thinking "I've done all the modules, I have good ears now" and leaving.

**5. Three months in.**
- A long streak displayed prominently.
- A profile dashboard with completed modules and their scores as visual proof of progress.
- A collection of unlocked guitar badges — iconic instruments owned by famous players (Hendrix's upside-down Strat, Angus Young's SG, Brian May's Red Special) earned through consistent daily use and longer streaks.
- **Real-world transfer.** Throughout progression the app prompts application outside itself — "try to work out part of a song on your guitar", "ask your teacher to test you on intervals". The end-state is not *app completed* but *ear training has bled into real musicianship* — when Ruairidh notices it is easier to figure things out by ear than it used to be.

---

## Constraints

**Quit triggers (hard limits — these are what make him leave):**
1. Feeling there is **nothing left to learn** — the "I have good ears now, I'm done" moment. Primary abandonment risk. The no-terminal-state module design is built to prevent this.
2. **Stopping guitar lessons or stopping playing guitar entirely** — if the instrument leaves his life the app loses its anchor.
3. **Feeling the ear training has no use case in his actual playing** — disconnection from real musicianship breaks the value proposition. The real-world transfer prompts fight this.

**NOT a quit trigger:** losing a streak does not crush him. The leaderboard and personal-best chase are heavier motivators than streak preservation — meaning the streak is gamification scaffolding, not load-bearing.

**Notifications.** Push reminders to keep a streak alive are acceptable ONLY if they can be turned off. Tamir's own annoyance threshold sets the bar.

**Audience reframe.** This is NOT a kids' app — it is an all-ages product that happens to be kid-friendly. Ruairidh represents the youngest demanding user the app must serve, not the target audience.

**Privacy posture (defensive).**
- No real names anywhere.
- No personal information beyond a chosen username.
- No email required.
- No password — profile-picker model with clickable usernames.
- Leaderboard names are made-up.

**Reading / typing constraints.**
- No long-form text anywhere.
- Multiple-choice answers only.
- Long explanations delivered via video, never text walls.
- Instructions are audio, video, or one to two sentences.

**Latency budget.**
- Hot path (existing user, existing module) — 5 to 10 seconds from phone-in-hand to first question.
- New-module path tolerates a short video intro at the start, but jumping straight back into a known module must be near-instant.

**Error UX.** "Try again" is the only error message Ruairidh should ever see — backend errors must never bubble up as technical text.

**Open regulatory question (for Theo at contract-mapping).** All-ages-but-kid-friendly positioning sits in a grey zone for the UK Age Appropriate Design Code, which applies when kids are likely to access regardless of intent. Privacy-first defaults are the right defensive posture but exact compliance scope — especially around leaderboards involving minors — needs confirmation.

---

## Paired Relationships

Ruairidh's behaviour intersects with two other roles. Neither is a separate persona yet, but the data boundaries matter for outcome design.

**Parents (access controllers, not co-users).** The parent hands the phone over and may have their own profile on the same install. The parent does NOT operate the app on Ruairidh's behalf, but DOES need to be able to:
- Set up Ruairidh's profile initially (one-time setup, then never again)
- Turn streak notifications off if they choose
- Be unobtrusive — the app should not nag the parent for permissions, emails, or attention beyond initial setup

**Other users on the leaderboard.** Ruairidh sees their made-up usernames and scores. They see his. **Nothing else flows between users.** No real names, no avatars derived from real images, no chat, no friend requests.

**Siblings on the same device.** Each has their own profile with separated progress, streak, and leaderboard position. A sibling tapping Ruairidh's profile icon would see his data — physical access to the phone is the only gate. This is acceptable in a family-device context but flags one outcome consideration: profile-switching from the home screen must be friction-light so siblings don't accidentally play under each other's profiles.

**Guitar teacher.** Lives entirely outside the app in current scope. No data flows in or out. The teacher is a *trigger source* (their lesson reminds Ruairidh to use the app) and a *real-world feedback recipient* (when the app prompts "ask your teacher to test you on intervals") — but the teacher does not log in, does not see Ruairidh's scores, and is not designed for. This may change in later phases if the product extends into teacher dashboards.

---

## Acid-Test Assessment

**Ruairidh is the acid-test persona.** His constraint stack:

- Most constrained reality — borrowed phone, 2–5 minute windows, phone-speaker audio, parent-controlled access
- Lowest prior knowledge — no theory, no fretboard names, no formal vocabulary
- Lowest self-motivation — ~85% parent-initiated baseline
- Strictest privacy posture — kid-friendly means no PII, no real names, no password
- Smallest acceptable error vocabulary — "try again" only
- Smallest text tolerance — multiple choice + video + 1–2 sentences max
- Tightest latency tolerance — 5–10 seconds to first question on a known module

If outcomes pass Ruairidh's verification steps, an adult hobbyist learning intervals on a longer evening session is trivially served as well. The reverse is not true.

---

## Open Design Questions Carried Forward

These are real questions that surfaced during persona work but belong further downstream. Marcus and Theo should pick them up.

1. **Within-module difficulty progression.** For binary discrimination tasks (e.g. major 2nd vs minor 2nd) there is no obvious "harder" once accuracy is high. Speed and playback-speed are two levers — is that enough? *Revisit with Marcus.*
2. **Vocabulary onboarding pathway.** At what point does Ruairidh move from "happy/sad" affective labels → "major/minor" formal labels → specific interval names ("major 3rd")? Is this driven by the app's structure, by his teacher, or both? *Revisit with Marcus.*
3. **Regulatory positioning.** All-ages-but-kid-friendly sits in a grey zone for the UK Age Appropriate Design Code. Privacy-first defaults are the right defensive posture but exact compliance scope (especially leaderboards involving minors) needs confirmation. *Flag for Theo at contract-mapping.*

---

*Build outcomes for Ruairidh first. If your outcomes pass Ruairidh's verification steps, everything downstream will hold.*
