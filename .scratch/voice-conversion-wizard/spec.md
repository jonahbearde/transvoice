Status: ready-for-agent
Feature: voice-conversion-wizard

# Voice conversion wizard

## Problem Statement

I have videos whose narration is spoken by someone whose voice does not fit the video — a male narrator on material that wants a female one, or simply a voice I am tired of hearing. There is no local tool that fixes this without destroying the video: existing voice changers are either research scripts with no interface, or they transform the *entire* mix so the music comes out sounding possessed, or they re-synthesize the speech and lose the narrator's pacing, emphasis, and stumbles. I want to hand a video to a local web page, pick a different voice, hear twenty seconds of what it will sound like, and get my video back with its picture untouched and its music intact.

## Solution

A locally hosted web app that performs a **conversion**: the video's narration is isolated from the bed, its timbre is changed to a target voice from a catalogue of imported presets, and the result is mixed back over the original bed and muxed under the original, unmodified picture. A four-step wizard — upload, choose a voice, preview, convert — with a preview short enough to audition voices repeatedly, and conversions that survive being walked away from.

The tool changes **who the narration sounds like** and nothing else. Pace, emotion, emphasis, and breathiness are the narrator's and stay the narrator's (ADR-0001). Voices are imported trained models rather than cloned from clips (ADR-0002).

## User Stories

**Getting set up**

1. As an editor, I want to install the tool on the machine with the GPU using one script, so that I do not have to assemble a Python environment by hand.
2. As an editor, I want a `setup` step that fetches the voice catalogue described by the shipped manifest, so that the wizard is not empty on first launch.
3. As an editor, I want the app to tell me clearly when ffmpeg or the converter's environment is missing, so that a first-run failure does not look like a bug in the tool.
4. As an editor, I want the app to report the detected GPU and tell me if it is below the supported floor, so that I know why a conversion is slow or why I am being warned.
5. As an editor, I want the app to bind to localhost only, so that I am not exposing my machine to my network.

**Importing voices**

6. As an editor, I want to drag a `.pth` file into a presets folder and have it appear in the wizard, so that I can add any voice I have found without editing configuration.
7. As an editor, I want an imported preset to be paired automatically with its `.index` file, so that I get the timbre fidelity the index provides without having to reason about filenames.
8. As an editor, I want an imported preset with no index to still work, with the tool automatically lowering the retrieval strength to zero and telling me it did so, so that a partial download is a degraded conversion rather than an error.
9. As an editor, I want an old-format checkpoint to still convert, so that a voice I have had for years is not refused.
10. As an editor, I want a preset trained with multiple speakers to default to its first speaker and show me the available ones, so that I can pick without the tool crashing.
11. As an editor, I want to give each imported preset a human label and timbre tags in a sidecar file, so that a filename like `KAKKOII` does not become the name of a voice in my interface.
12. As an editor, I want the importer to accept a file it cannot fully parse rather than refuse it, while telling me what it could not determine, so that an unknown checkpoint is still worth trying.
13. As an editor, I want to see which presets are installed and how much disk they occupy, so that importing fifty voices does not silently eat gigabytes.
14. As an editor, I want to remove a preset without the tool breaking, so that I can prune a catalogue I over-imported.
15. As an editor, I want a preset whose label uses a delivery adjective to be rejected at import with an explanation, so that the catalogue never promises something the tool cannot deliver.

**Uploading and preparing**

16. As an editor, I want to drop a video file onto the page and start the wizard immediately, so that I do not need to pick an output format before I have heard anything.
17. As an editor, I want the tool to tell me the video's duration, resolution, and detected speakers before I commit, so that I know what I am about to wait for.
18. As an editor, I want the tool to isolate the narration from the bed automatically, so that the music and effects survive the conversion unconverted.
19. As an editor, I want the tool to skip isolation when the audio is already clean speech, and to tell me it skipped it, so that a music-free video does not pay for a stage it does not need.
20. As an editor, I want a quality toggle for the isolation stage, so that a dense music bed can buy a better split at the cost of time.
21. As an editor, I want to be able to say "this audio is only speech" manually, so that I can override the automatic decision when it guesses wrong.
22. As an editor, I want a video containing no speech to be rejected with a clear message, so that I am not waiting for a conversion of silence.

**Choosing a voice**

23. As an editor, I want the preset list to load from disk instantly, so that choosing a voice is never gated behind processing.
24. As an editor, I want presets grouped by their tags rather than dumped as a flat list, so that a large catalogue is browsable.
25. As an editor, I want to see, for each preset, roughly what pitch it lives at, so that I can reject an obviously wrong choice before spending time on a preview.
26. As an editor, I want the tool to retune the narration to the chosen preset's pitch automatically, so that a male-to-female conversion does not come out sounding like a woman with a man's voice.
27. As an editor, I want a simple higher/lower control to override that retuning, so that I can correct an automatic decision that sounds wrong.
28. As an editor, I want to see the semitone value behind that control, so that a choice I like is reproducible.
29. As an editor, I want a per-preset formant adjustment that defaults to off, so that a conversion carrying the narrator's chest resonance has a fix available without that fix being applied to every other voice.

**Previewing**

30. As an editor, I want the tool to pick the first clean stretch of narration automatically, so that previewing costs me no decisions.
31. As an editor, I want to adjust the start and end of the previewed excerpt, so that I can audition a voice on a passage I actually care about.
32. As an editor, I want the preview to complete in seconds, so that I can audition many voices before committing to one.
33. As an editor, I want to hear the preview mixed over the real bed rather than dry, so that I am judging what the output will actually sound like.
34. As an editor, I want to keep the preview after choosing a different voice, so that I can compare two voices without the first one being thrown away.

**Converting**

35. As an editor, I want to start the full conversion and leave the page, so that a thirty-minute video is not a thirty-minute vigil.
36. As an editor, I want to see which stage the conversion is in and how far through it is, so that a long wait is distinguishable from a hang.
37. As an editor, I want the conversion to split the narration on silence and work through it in pieces, so that a failure near the end does not cost me the whole video.
38. As an editor, I want to refresh the page mid-conversion and find the conversion still running, so that a browser reload is not a cancel.
39. As an editor, I want to cancel a conversion and have it actually stop, so that I can reclaim the GPU for something else.
40. As an editor, I want a failed conversion to tell me which stage failed and why, so that I can tell "my preset is bad" from "my video is unusual".
41. As an editor, I want to remain able to use the tool while a conversion runs, so that one long conversion does not lock the interface.
42. As an editor, I want a warning when the video appears to contain more than one speaker, so that I understand the result will make everyone sound like the same person.

**Getting the output**

43. As an editor, I want the output as a video file whose picture is bit-for-bit the input's picture, so that I do not lose quality re-encoding footage I already paid to encode.
44. As an editor, I want the converted narration as the default audio track, so that the file plays correctly in any player.
45. As an editor, I want the original narration preserved as a second audio track, so that I can A/B the result without returning to the tool.
46. As an editor, I want the output's duration to equal the input's exactly, so that the file drops into an editor without shifting.
47. As an editor, I want the isolated narration, the converted voice, and the bed exported separately, so that I can diagnose a bad result instead of only rejecting it.
48. As an editor, I want a record of every parameter used in a conversion, so that a result I like can be reproduced and a result I dislike can be explained.
49. As an editor, I want to run a second conversion of the same video with a different voice without re-uploading or re-isolating it, so that auditioning at full length is not wasteful.
50. As an editor, I want output files named after the source video and the voice used, so that twenty conversions do not become `output_1.mp4` through `output_20.mp4`.

**Debugging and trust**

51. As an editor, I want an advanced disclosure exposing how strongly the preset's voice is copied and how strongly unvoiced consonants are protected, so that a conversion with mushy S sounds or a weak resemblance is fixable.
52. As an editor, I want those two knobs explained in plain language rather than by their upstream names, so that I do not need to read RVC's source to use them.
53. As an editor, I want the tool's default parameter values pinned rather than inherited from the converter's defaults, so that an upstream update cannot silently change my results.
54. As an editor, I want the tool to refuse to overwrite an existing output file without asking, so that a re-run does not destroy the take I liked.

## Implementation Decisions

**Pipeline.** A single conversion entry point takes a source video, a preset, and options, and returns a conversion record. Stages, in order: probe the source; extract audio without decoding video; isolate the narration stem from the bed unless skipped; detect speech and split the narration stem into chunks on silence; convert each chunk through the converter port; apply the preset's formant offset if non-zero; concatenate and force the narration to the original's exact duration; mix the converted narration over the bed with gain matched to the original narration's loudness; mux with the video stream copied and both audio tracks present. Stage boundaries are recorded per chunk so a conversion resumes rather than restarts. A single sequential worker owns conversions; the interface stays responsive because conversions never run in a request.

**Converter port.** An interface with one operation: convert a chunk given a preset reference, a retune in semitones, and the pinned parameter set. Two implementations: an adapter that shells out to RVC's offline CLI in a separately managed environment, and a stand-in that performs a pitch-and-formant shift in-process. The port translates subprocess outcomes into failure kinds — bad preset, out of memory, crashed, timed out — because the pipeline branches on those and never on stderr text (§ADR-0003).

**Pinned parameters.** The retrieval strength, voiceless-consonant protection, loudness envelope mixing, filter radius, and pitch extractor are fixed by the application and written into every conversion record. Upstream defaults are never inherited: the two candidate upstreams disagree on retrieval strength by a factor of 2.5, and pitch extractors that older documentation still advertises no longer exist. Only retrieval strength and voiceless-consonant protection surface in the interface, behind a disclosure (§ADR-0001, §ADR-0003).

**Preset registry.** Presets live in a folder as a checkpoint, an optional retrieval index, and a sidecar carrying the display label, timbre tags, and formant offset. The registry parses each checkpoint for format version, pitch-awareness, and speaker list; resolves index pairing itself rather than trusting filenames; and derives an effective retrieval strength of zero when no index resolves. Labels are validated against the glossary's rule that delivery adjectives are not timbre (§ADR-0002). A shipped manifest lists remotely hosted presets with their labels and tags, fetched by an explicit setup command — no voice weights are distributed with the repository.

**Conversion record.** Persisted per conversion and serves as the wizard's only state: source reference, preset reference, resolved parameters, per-chunk status, stage reached, artifact paths, failure kind and message, and timestamps. Resumability, page-reload survival, and the parameter log are all reads of this record rather than separate mechanisms.

**Chunking.** Chunks are cut on detected silence with a minimum silence duration, never mid-word, with padding on each side. A chunk exceeding a size budget is subdivided. The number of chunks and their boundaries are recorded so a resumed conversion skips completed ones.

**Duration and levels.** Output audio duration equals the narration's original duration exactly, by trimming or padding the reassembled narration. The converted narration is gain-matched to the original narration's loudness before mixing, because the isolation stage rescales its stems and would otherwise shift the balance between voice and bed.

**Web surface.** Server-rendered wizard, one step per view, with progress delivered as server-sent events and no build step. Routes for upload, step views, preset listing and import, preview creation, conversion start and cancel, artifact download, and the event stream. Preset choice is gated on isolation completing, so the wizard is strictly linear.

**Configuration.** Catalog folder, working folder, RVC environment path, model and index roots, the device the pipeline expects, and the pinned parameter set — all in one place, overridable for the stand-in converter so the pipeline runs without a GPU.

## Testing Decisions

**Seam 1 — the conversion entry point.** The highest point below the interface: one call in, a record and files out. Tests assert only externally observable facts: output duration equals input duration; the output carries two audio tracks; the narration stem, converted voice, and bed all exist; the record contains the resolved parameters and per-chunk statuses; a truncated rerun resumes rather than recomputing; a source with no speech fails with the no-speech kind. Nothing asserts on stage internals, intermediate sample counts, or how many processes were spawned.

**Seam 2 — the HTTP application.** Driven through an ASGI test client: upload creates a conversion, the wizard advances step by step, a preset can be imported and appears in the listing, a preview is produced and retrievable, conversion start yields progress events, and artifacts download by identifier. A conversion started, then re-fetched by identifier after a simulated reload, still reports its stage. Assertions are on status codes, presence of rendered fragments, and the shape of event payloads — never on HTML structure or class names.

**Substitution point — the converter port.** Bound to the stand-in for all automated tests, so the suite runs on a machine with no usable GPU. The stand-in must genuinely transform audio (pitch shift) so downstream stages cannot pass by echoing their input; a second fake raises each failure kind so the pipeline's error and resume paths are reachable.

**What makes a good test here.** A good test states a property a user could check with a media player: the file plays, it is the same length, the second audio track is still there, the voice is different, the bed is not. A bad test knows which stage ran, how many chunks were cut, or what the parameter object looked like internally. The chunking policy, the isolation adapter, the formant stage, and the mixer deliberately have no tests of their own — their behaviour is observable at seam 1, and giving each a seam would raise the count from three to seven to test things a user cannot perceive directly.

**Fixtures.** A committed script synthesizes the fixture media with ffmpeg rather than committing binaries: a short clip of speech-like tone over a music bed, a short clip of speech alone, a short clip with two alternating voices, and a ninety-second clip that forces multiple chunks. Fixtures are regenerated on demand and are small enough to keep the repository light.

**Prior art.** None — this is the first code in the repository. The conventions established here are the prior art: pytest, tests that drive the two seams, and no network access and no real converter in the automated suite.

## Out of Scope

- Changing delivery, emotion, pace, or emphasis (ADR-0001). The tool cannot make a narration gentle, warm, or calm.
- Cloning a voice from a user-supplied reference clip (ADR-0002).
- Training presets, synthesizing training data, or shipping voice weights in the repository.
- Re-voicing from a transcript (ASR → TTS) in any form.
- Speaker diarization or converting different speakers into different voices; multi-speaker audio is converted uniformly and warned about.
- On-camera lip-sync guarantees; timing is preserved, but the picture is not inspected.
- AMD and Intel GPU support; the supported floor is an 8 GB NVIDIA card.
- Multi-user access, authentication, remote conversion over the network, and containerized deployment.
- Batch conversion of a folder of videos, and any form of queue prioritization.

## Further Notes

Build order is chosen so that everything except the converter is provable on a CPU-only machine: probe, extract, isolate, chunk, assemble, mix, mux, the record store, the worker, and the whole wizard all run locally today, with the stand-in converter in place of RVC. The converter adapter and the pinned-parameter tuning are the only parts that require the GPU machine, and they sit behind the port so they can be validated last.

Decisions worth re-reading before starting: ADR-0001 fixes the product's promise and its limits, ADR-0002 explains why the importer exists and why cloning does not, ADR-0003 explains the subprocess seam and why the stand-in converter is permanent. `CONTEXT.md` fixes the vocabulary — narration, bed, narration stem, timbre, delivery, retuning, target voice, preset, conversion, preview, output video — and the spec above uses those words deliberately. The rule that presets are never labelled with delivery adjectives is enforced in code, not in documentation alone.