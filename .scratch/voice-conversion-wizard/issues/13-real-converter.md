# 13: The real converter

**What to build:** The product actually changing someone's voice. The stand-in is replaced by the adapter that drives RVC's offline command-line interface as a child process in its own environment, never imported into the application. The chosen preset, the automatic retune, and the pinned parameters are all honoured, and each upstream failure — bad preset, out of memory, crash, timeout — surfaces as its own actionable message rather than as a wall of stderr. This is the only ticket whose acceptance requires the GPU machine.

**Blocked by:** 03, 06, 12

**Status:** ready-for-agent

- [ ] Selecting a preset changes the narration's timbre, verified by ear on a real video and by pitch and timbre measurements
- [ ] The preset, the retune in semitones, and every pinned parameter reach the converter and the resulting values appear in the record
- [ ] The converter runs as a child process in its own environment, and the application never imports it
- [ ] A bad or unreadable preset, an out-of-memory condition, a crash, and a timeout each produce a distinct failure kind with an actionable message
- [ ] A five-minute video converts without exhausting an 8 GB card, and a deliberately oversized chunk produces the out-of-memory failure kind rather than a hang
- [ ] The automated suite still runs on a machine without a GPU, because the port's stand-in remains bound there
- [ ] Validated on the GPU machine before merge, with the wall-clock time for a five-minute video recorded for comparison against the stand-in