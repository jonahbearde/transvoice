# 10: Multi-speaker warning

**What to build:** An honest warning before a conversion that will produce a surreal result. When the narration appears to contain more than one speaker, the wizard says so before the conversion starts, explaining that every speaker will end up sounding like the same person. The warning is recorded on the conversion and never blocks it — converting anyway is a valid choice.

**Blocked by:** 04

**Status:** ready-for-agent

- [ ] A fixture containing two alternating voices triggers the warning before conversion begins
- [ ] A single-voice fixture does not trigger the warning
- [ ] The warning explains the consequence in terms of the target voice, not in terms of audio processing
- [ ] Conversion proceeds normally after the warning, and the warning is recorded on the conversion
- [ ] Speech detection never invents a warning on a single-voice source with background music present