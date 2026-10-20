# Presets are trained voice models, not reference samples

Status: accepted

Every target voice in the catalogue is a trained RVC checkpoint on disk — a `.pth` plus an optional `.index` retrieval index, roughly 55 MB and 30 MB respectively. The tool does not clone a voice from a short clip. We rejected zero-shot reference-sample conversion because the engine we chose for output quality has no reference path at all, and we rejected generating our own presets because producing one costs hours of GPU time per voice against unpublished evidence that synthetic training data produces acceptable results.

## Consequences

- There is no "drop in a 10 second clip" feature, and its absence is deliberate. A future reader looking at the importer will wonder why the obvious convenience is missing: adding it means adding a second engine, not adding an upload button.
- The catalogue grows only by import. Variety is a property of what exists on the internet, not of anything we ship, and the first-run experience depends on a fetchable manifest rather than on bundled weights.
- Sample rate, loudness, and the presence or absence of the retrieval index are all properties of a file somebody else trained, so the importer must adapt to them rather than reject them.
- Executing a conversion requires both the checkpoint and its index to survive the round trip; an index that is present but named `trained_*` instead of `added_*` is silently ignored upstream, so the importer resolves index paths itself rather than trusting filenames.