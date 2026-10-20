# 05: Chunk on silence, survive interruption

**What to build:** Long conversions that can be walked away from. The narration is split into chunks at detected silence — never mid-word, with a minimum silence duration and padding on each side — and each completed chunk is recorded so a conversion that dies near the end resumes instead of restarting. Progress is reported per stage and per chunk. A browser reload leaves the conversion running and still shows its stage, and cancelling actually stops it.

**Blocked by:** 02

**Status:** ready-for-agent

- [ ] A ninety-second source converts in more than one chunk, with chunk boundaries and count recorded
- [ ] Every chunk boundary falls inside detected silence, verified against the fixture's known silence positions
- [ ] A conversion interrupted after some chunks complete resumes and skips the completed ones on rerun
- [ ] Progress events report the current stage and the count of completed chunks
- [ ] Reloading the wizard mid-conversion shows the conversion still running and at its current stage
- [ ] Cancelling a running conversion stops work promptly and marks the conversion cancelled rather than failed
- [ ] A converter that fails on a middle chunk leaves earlier chunks completed and the failure attributed to that chunk