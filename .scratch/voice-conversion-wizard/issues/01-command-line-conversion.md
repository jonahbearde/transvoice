# 01: Convert a video end to end, from the command line

**What to build:** A conversion that runs from a terminal command and produces a real output video. The source's picture is copied through untouched, the narration is extracted, passed through the stand-in converter (which genuinely shifts pitch, so downstream stages cannot pass by echoing their input), reassembled to exactly the original duration, and muxed back with the converted narration as the default track and the original narration as a second track. Every conversion writes a record containing the resolved parameters and the artifacts it produced. This is the tracer bullet: it establishes the pipeline entry point and the conversion record that everything later reads from.

**Blocked by:** None (can start immediately)

**Status:** ready-for-agent

- [ ] Converting a short speech-only video yields an output video whose video stream is copied rather than re-encoded, playable in a normal player
- [ ] The output's duration equals the input's duration exactly
- [ ] The output carries two audio tracks: converted narration first, original narration second
- [ ] The converted audio is measurably different in pitch from the original, proving the stand-in converter was actually invoked
- [ ] A conversion record is written containing the resolved parameter set, artifact locations, and timing, and is readable without the interface
- [ ] A committed script generates the fixture media with ffmpeg, and the seam-1 tests run end to end with no GPU and no network