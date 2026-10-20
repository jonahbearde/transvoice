# 11: Re-convert without re-isolating

**What to build:** Auditioning at full length without paying for isolation twice. After a completed conversion, running a second preset against the same video reuses the cached narration stem and bed, so the second conversion starts already past the expensive stage. Outputs are named for the source video and the preset used, and an existing output is never silently overwritten.

**Blocked by:** 04, 05

**Status:** ready-for-agent

- [ ] A second conversion of the same video with a different preset skips isolation and records that the cached stems were reused
- [ ] The second conversion's output differs from the first's wherever the presets differ
- [ ] Outputs are named after source and preset, so repeated conversions do not collide into numbered filenames
- [ ] An existing output file is never overwritten without an explicit confirmation, and the refusal is visible
- [ ] Artifacts from both conversions remain individually downloadable after the second completes
- [ ] Cached stems are attributable to a specific source, so a different video never reuses them by accident