# 09: Advanced disclosure

**What to build:** An escape hatch for conversions that come out weak or mushy. Behind a disclosure, two controls — how strongly the preset's voice is copied, and how strongly unvoiced consonants are protected — described in plain language rather than by their upstream names, with the underlying numbers shown. Changing them affects the next conversion and is recorded, so a fixed result is reproducible. They are absent from the default path so first-time users never see them.

**Blocked by:** 06

**Status:** ready-for-agent

- [ ] The disclosure exposes exactly those two controls, in plain language, with their numeric values visible
- [ ] The controls are not present on the default path until the disclosure is opened
- [ ] Changing a control affects the next conversion and the new value appears in that conversion's record
- [ ] An out-of-range value is rejected with a message rather than silently clamped
- [ ] Tests assert the recorded values and the resulting audio behaviour, not the markup of the disclosure