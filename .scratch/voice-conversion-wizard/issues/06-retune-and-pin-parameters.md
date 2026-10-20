# 06: Retune to the target voice, and pin the parameters

**What to build:** The stage that stops a female timbre from coming out sounding like a man. Each conversion retunes the narration toward the chosen preset's pitch automatically, derived from the narrator's pitch and the preset's, with a higher/lower override in the wizard and the semitone value visible for reproducibility. At the same time, the five quality parameters that decide whether a conversion sounds broken are fixed by the application rather than inherited from the converter's defaults, and are written into every conversion record.

**Blocked by:** 03

**Status:** ready-for-agent

- [ ] Converting a male narrator into a higher-pitched preset records a non-zero automatic retune and produces measurably higher pitch than an unconverted pass
- [ ] The wizard's higher/lower override changes the recorded semitone value and audibly changes the result
- [ ] The semitone value is displayed, not hidden behind the override control
- [ ] All five pinned parameters appear in the conversion record with application-chosen values
- [ ] Changing the application's configured defaults changes the recorded values, proving they are not inherited from the converter
- [ ] Pitch contour and rhythm are unchanged by retuning, while the pitch median moves