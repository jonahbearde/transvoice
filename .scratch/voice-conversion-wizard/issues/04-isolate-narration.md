# 04: Isolate the narration from the bed

**What to build:** The stage that makes the output usable. A video with music comes back with its music intact and un-converted, because the narration is separated from the bed before conversion and mixed back afterwards. The narration stem, the converted voice, and the bed are all exported as separate files so a bad result can be diagnosed. When the audio is already clean speech the stage is skipped and the record says so; a quality toggle buys a better split for dense beds, a manual override forces the decision either way, and a source containing no speech is rejected with a clear message.

**Blocked by:** 02

**Status:** ready-for-agent

- [ ] A video with a music bed converts with the bed preserved — the output's bed is the same audio as the separated bed, not run through the converter
- [ ] Narration stem, converted voice, and bed are exported as separate downloadable artifacts
- [ ] A clean-speech video skips isolation, and the record marks the stage as skipped rather than completed
- [ ] The quality toggle selects a different separation setting and the record shows which was used
- [ ] A manual "this audio is only speech" override is honoured even when automatic detection disagrees
- [ ] A source containing no speech fails with a no-speech failure kind and an actionable message
- [ ] Seam-1 tests cover both the music-bed and speech-only fixtures