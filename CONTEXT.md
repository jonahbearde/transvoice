# Transvoice

A local tool that changes **who a video's narration sounds like** without changing what it says or how it says it. This glossary fixes the vocabulary the project reasons in; it deliberately records no design or implementation.

## The speech

**Narration**:
The spoken content of a source video that the tool converts. Assumed to be a single speaker and not lip-synced, because the source video's picture is never touched.
_Avoid_: Voiceover, VO, dialogue, speech track

**Bed**:
Everything in the source audio that is not narration — music, sound effects, room tone, laughter.
_Avoid_: background, music track, ambience, leftover

**Narration stem**:
The narration, isolated from the bed, as a separate audio signal.
_Avoid_: vocals, vocal track, acapella — that is music-separation terminology, and a separator's "vocals" stem is trained on singing, not on speech

## What changes, and what doesn't

**Timbre**:
The identity of a voice: what makes two speakers of the same language, saying the same words at the same pitch, read as different people. **Timbre is the only thing this tool changes.**
_Avoid_: voice (unqualified), tone, colour, accent

**Delivery**:
How the narration is performed — pace, pauses, pitch range, energy, breathiness, emotion.
_Avoid_: prosody, style, tone, performance, mood. **"Gentle", "warm", "calm", "excited" are delivery words and are therefore not reachable targets for this tool** — a delivery adjective on a preset is a bug in the preset's name.

**Retuning**:
Shifting the narration's pitch without changing its delivery (its pitch *contour* and rhythm stay as performed). Distinct from retiming, which this tool never does.
_Avoid_: pitch shift (unqualified), transpose, formant shift

## The target voice

**Target voice**:
The voice the narration is converted into. A target voice has a timbre and nothing else — no delivery, no words, no language.

**Preset**:
A target voice that ships with the tool rather than being supplied by the user. A preset is a trained voice model, not a recording — the tool never clones a voice from a single clip.
_Avoid_: reference sample, voice clip, prompt, built-in voice, default voice

## The work

**Conversion**:
One pass that turns a source video plus one target voice into an output video.
_Avoid_: job, run, task, process, render

**Preview**:
A conversion restricted to a short excerpt of the narration, used to decide whether a target voice is worth a full conversion.
_Avoid_: sample, test, draft, audition

**Output video**:
The result: the source video's picture, unchanged, with the converted narration mixed back over the bed.
_Avoid_: rendered video, result, dub