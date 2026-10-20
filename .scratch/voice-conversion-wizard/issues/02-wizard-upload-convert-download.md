# 02: The wizard — upload, convert, download

**What to build:** The product's interface, as a strictly linear wizard over the pipeline from ticket 01. A video is dropped on a page, a conversion is created and starts running in a worker that is not the request, the page shows which stage the conversion has reached and keeps showing it without a manual reload, and the finished output video downloads by identifier. A second upload while a conversion runs is accepted and queued rather than blocked. Server-rendered, no build step.

**Blocked by:** 01

**Status:** ready-for-agent

- [ ] Dropping a video creates a conversion and advances the wizard to the next step
- [ ] The page reports the conversion's stage and updates it without a manual page reload
- [ ] The finished output video downloads by identifier and plays
- [ ] The interface stays responsive while a conversion runs, and a second upload is accepted rather than dropped
- [ ] Seam-2 tests drive upload, status, and download through the application's HTTP surface, asserting on responses and event payloads rather than on markup
- [ ] A conversion that fails reports a failure kind and message that distinguishes the cause from an internal error