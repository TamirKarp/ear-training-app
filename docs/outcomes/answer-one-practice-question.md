# Outcome 1: Answer One Practice Question

> Approved by Tamir on 2026-06-10. Four-trap quality review passed.
> Acid-test persona: Ruairidh. See `docs/personas/ruairidh.md`.
> Terminology reconciled 2026-06-24: leaf-level exercises are **elements** within **modules** (Intervals → Major & Minor 3rds). The question bank lives at the element level. See Outcome 2.

---

## Field 1: Persona
**Ruairidh** — mid-Practice session on a parent's phone played through the built-in speaker, two to three minutes into one of his typical short windows (car, waiting, after-dinner), looking at the screen ready for the next question with no particular emotional charge.

See: `docs/personas/ruairidh.md`

---

## Field 2: Trigger
A new Practice question is presented to Ruairidh — either the first question of the session, or the next question after a previous answer has been resolved.

A "previous answer has been resolved" means: the correct button was tapped, the confirmation audio played, and the auto-advance delay elapsed.

---

## Field 3: Walkthrough

The question screen appears. The question audio plays automatically — for an interval element, two notes played in sequence, roughly two to three seconds total.

Below the audio area, the multiple-choice answer buttons render. The number of buttons depends on the element: two for a binary discrimination like major-2nd-versus-minor-2nd, three or four for a wider set. The buttons are active from the moment they appear — Ruairidh can tap an answer before the question audio has finished playing if he is confident. His tap cuts the question audio; the feedback flow begins immediately.

A replay button is visible on screen. Ruairidh can tap it as many times as he wants to hear the question audio again. There is no limit. The replay button is available throughout the answering process, including during any wrong-tap loops, and disappears only after he taps the correct answer.

Ruairidh taps a button. The system registers whichever tap arrived first as his attempt.

**If his tap is correct:** the tapped button turns green. The question audio plays one more time as a confirmation of what the correct answer sounds like. The replay button is no longer visible during this confirmation. When the confirmation audio finishes, an auto-advance delay begins — on the order of one to two seconds. When the delay completes, the trigger for the next Practice question fires, and this outcome ends.

**If his tap is wrong:** the tapped button turns red and stays red. The audio of what *the wrong button he tapped* represents plays — so he hears that interval or chord, alongside the memory of what he was actually asked to identify. When the wrong-button audio finishes, the screen returns to a ready-for-another-tap state. All other buttons remain active. The correct answer is NOT revealed. The replay button is still visible. Ruairidh taps another button, and the loop continues.

The outcome only ends when Ruairidh taps a correct answer. Wrong taps loop within the question. Every wrong button he tapped during the question stays visibly red as a record of what he ruled out — so by the time he finds the right answer, he sees green on the correct button and red on every wrong one he tried.

---

### Failure paths

**If the question audio fails to load:** the question screen appears but no audio plays. A visual indicator shows audio failed. The answer buttons are disabled — Ruairidh cannot tap anything until audio plays successfully, because otherwise he would be guessing blind. The replay button retries the audio fetch. After three failed retries, the question is silently replaced with a different question on the same element, accompanied by a brief "Trying another one" message.

**If Ruairidh accidentally taps two buttons at the same time:** the system registers whichever tap arrived first as his attempt. The second tap is ignored regardless of whether the first was right or wrong. This protects against accidental double-tap burning through attempts on a small phone screen.

**If a phone notification interrupts the audio mid-playback:** audio pauses or stops depending on platform behaviour. Tapping the replay button restarts the audio cleanly from the beginning. If the interruption happens during the wrong-button audio playback, Ruairidh can simply tap another button — the screen remains functional whether the audio finishes or not.

**If the parent yanks the phone away before Ruairidh has tapped any button:** no answer is registered. When he returns to the app later, the same Practice question is re-presented from the beginning. The session-save outcome (separate, not yet written) is responsible for persisting which question was in flight.

**If the parent yanks the phone away after a wrong tap but before a correct one:** the same question reloads on session resume, with his prior wrong taps still visibly red. He continues from exactly where he left off. (The session-save outcome is responsible for snapshotting which buttons were tapped wrong, in what order.)

**If the parent yanks the phone away after the correct tap, during the confirmation audio or auto-advance delay:** the correct answer was registered. Practice keeps no score so there is no scoring impact. On session resume, the next question loads naturally — this question is complete.

---

## Field 4: Verification

1. When a new Practice question loads, the question's audio plays automatically without Ruairidh needing to tap anything.

2. The multiple-choice answer buttons appear on screen, ready to tap, no later than the moment the audio starts playing.

3. A replay button is visible on screen and tapping it plays the question audio again — Ruairidh can tap it as many times as he wants before answering.

4. When Ruairidh taps an answer that is correct, that button turns green.

5. After a correct tap, the question audio plays one more time as confirmation. The replay button is no longer visible during this confirmation.

6. After the confirmation audio finishes, the screen automatically advances to the next question within roughly one to two seconds — Ruairidh does not need to tap anything.

7. When Ruairidh taps an answer that is wrong, that button turns red, and the audio of what that wrong button represents plays so he can hear it.

8. After tapping a wrong answer, the correct answer is NOT revealed — Ruairidh can immediately tap any other button to try again.

9. The replay button remains visible and functional after a wrong tap, so Ruairidh can replay the original question audio before his next attempt.

10. Every wrong button Ruairidh taps during a single question stays visibly red, so by the time he finds the correct answer he can see a record of what he ruled out.

11. If the question audio fails to load, no answer button can be tapped until audio plays. Tapping the replay button retries the audio fetch.

12. After three consecutive failed attempts to play the question audio, the screen briefly shows "Trying another one" and a different question on the same element loads in its place.

13. If Ruairidh accidentally taps two buttons at the same time, the system treats only the first-arrival tap as his attempt. The second tap is ignored regardless of whether the first was right or wrong.

14. If a phone notification interrupts the audio playback, tapping the replay button restarts the audio cleanly from the beginning — Ruairidh is not stuck.

15. If the phone is taken away and Ruairidh returns to the app later, this specific question is preserved with his prior wrong-tap state intact (red buttons remain red). Verifying this is the responsibility of the session-save outcome; listed here for cross-reference.

**Notes for the QA agent:**
- Items 1–10 are testable in a browser using Playwright (load element, simulate taps, inspect button states, assert audio playback).
- Items 11, 12, 14 require simulating audio-load failure and notification interruption — testable in a browser with appropriate mocks.
- Item 13 (simultaneous tap) is genuinely hard to simulate without dual-touch hardware. May be deferred to integration testing on a real device, with browser tests covering the "rapid sequential tap" approximation.
- Item 15 is verified by the session-save outcome, not this one.

---

## Field 5: Contracts Exposed

**A "Practice question completed" signal:**
- The system now knows Ruairidh tapped a correct answer on a Practice question in the current session.
- The signal carries the timestamp of completion and identifies which element the question came from.

Consumed by:
- **Streak advancement outcome** — to determine whether this was the first activity of the day and therefore whether the streak should increment.
- **Session activity counter** — to track that one more question was completed in this session, for any session-level surfacing (e.g. "you've answered X questions today").

**A "ready for next Practice question" trigger:**
- The system signals that the current question's lifecycle is complete and the next Practice question can be presented.

Consumed by:
- The next instance of this same outcome — the loop that makes a Practice session a session, rather than a single question.

**Deliberately NOT exposed:**
- No persisted score (Practice keeps no score by design).
- No wrong-attempts record (the fact he took three attempts before getting it right is not stored).
- No leaderboard impact (Practice activity does not affect leaderboard rank — that is Test mode's job).
- No persisted in-flight question state (the session-save outcome handles snapshotting current question + wrong-tap state on session interruption, not this outcome).

---

## Field 6: Dependencies

- **Active Practice session on a specific element** — the Start a Practice session outcome (Outcome 2) must have started the session, and it must not yet have ended. This outcome cannot fire from a cold start.
- **The element's question bank is loaded** — audio files for each question, button labels for each answer option, and the mapping of which buttons are correct for each question. This is content / configuration provided by the content-loading outcome (also separate).
- **The audio playback system is functional** — the phone speaker can play audio and the audio file decoder is working. Platform infrastructure, not domain.
- **The current question has been selected and queued for presentation** by the Start a Practice session outcome (Outcome 2).

This outcome can be built once Outcome 2 (Start a Practice session) and the content-loading outcome are both at least drafted, but it cannot be verified end-to-end until those outcomes are also implemented.

---

## Forward notes for the next outcome

Logged during this outcome's writing — relevant when we write the Test-question outcome and the session-save outcome.

**Test-mode attempt rules (for the Test-question outcome):**
- Binary discrimination questions (2 options): 1 attempt only. Correct answer revealed after first attempt regardless of outcome.
- Non-binary questions (3+ options): 2 attempts allowed. Correct answer revealed after second attempt regardless of outcome.
- Test mode IS timed; Practice mode is not.
- No pause button in Test mode — would let users cheat the leaderboard.

**Same-question-on-resume rule (for the session-save outcome):**
- When a Practice session is interrupted mid-question, the same question must reload on resume with prior wrong-tap state preserved (red buttons stay red).
- The session-save outcome is the one responsible for this persistence — this outcome only consumes the queued question and produces the completion signal.

---

*Build outcomes for Ruairidh first. If this outcome passes Ruairidh's verification steps on a phone-speaker borrowed phone in a 2–5 minute window, the atomic interaction at the heart of the app is solid.*
