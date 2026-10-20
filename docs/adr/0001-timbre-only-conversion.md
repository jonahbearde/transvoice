# Conversion changes timbre only; delivery is inherited from the narrator

Status: accepted

A conversion changes **who the narration sounds like** and nothing else. Timbre is the only thing that moves; delivery — pace, pauses, pitch range, energy, breathiness, emotion — is inherited unchanged from the narrator. We rejected ASR → TTS re-voicing, the only pipeline that can set delivery, because it replaces the original performance, introduces transcription errors into the narration, and requires time-fitting every segment back into its original slot.

## Consequences

- "Gentle", "warm", "calm" are unreachable targets. Presets must never be named or described with delivery adjectives; the glossary forbids it. If a user asks for a gentle female voice, the honest answer is that this tool cannot make anyone gentle — it can only make them sound like someone else.
- Cross-gender conversion is not timbre-only in practice: a female timbre carrying a male narrator's pitch reads as male, so every conversion retunes pitch to the target's range. Retuning shifts pitch while leaving the contour and rhythm as performed.
- RVC exposes no formant control, so a conversion can carry the narrator's chest resonance inside the target's timbre. A per-preset formant offset exists to compensate, defaulting to zero.
- If delivery ever becomes a requirement, this is the ADR to supersede, and the replacement engine is a TTS re-voicing pipeline, not a better voice converter.