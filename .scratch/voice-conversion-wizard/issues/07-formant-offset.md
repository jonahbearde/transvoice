# 07: Per-preset formant offset

**What to build:** A fix for conversions that carry the narrator's chest resonance inside the target's timbre, since the converter offers no formant control of its own. A preset's sidecar may carry a formant offset; when it is non-zero the converted narration's spectral envelope is shifted after conversion while pitch is left alone. The offset defaults to zero, so every imported preset behaves exactly as it did before until someone deliberately turns it on.

**Blocked by:** 03, 06

**Status:** ready-for-agent

- [ ] A preset with a zero offset produces output indistinguishable from a build without the formant stage
- [ ] A preset with a non-zero offset produces a measurably shifted spectral envelope while the pitch median is unchanged
- [ ] The applied offset is recorded in the conversion record
- [ ] The offset is stored with the preset and applied automatically on every conversion using it, with no per-conversion control needed
- [ ] A formant stage failure is reported as its own failure kind rather than corrupting the output silently