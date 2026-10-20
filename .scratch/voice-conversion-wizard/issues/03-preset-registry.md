# 03: Preset registry and picker

**What to build:** The catalogue of target voices. Dropping a checkpoint into the catalogue folder makes it appear in the wizard without restarting the app, paired automatically with its retrieval index when one exists, labelled by a sidecar file rather than by its filename. A preset with no index still converts, with the tool lowering retrieval strength to zero and saying so. Old-format checkpoints are accepted, and a multi-speaker checkpoint defaults to its first speaker while showing the others. The chosen preset is recorded in the conversion record and reaches the converter port.

**Blocked by:** 02

**Status:** ready-for-agent

- [ ] A checkpoint dropped into the catalogue appears in the picker without an app restart
- [ ] An index file is paired with its checkpoint by inspection, not by trusting its filename, and a checkpoint whose index exists but is misnamed still retrieves
- [ ] A checkpoint with no index converts successfully, with effective retrieval strength recorded as zero and the fact surfaced to the user
- [ ] An old-format checkpoint is accepted and converts
- [ ] A multi-speaker checkpoint defaults to its first speaker and lists the available speakers
- [ ] The sidecar supplies the display label and timbre tags; an unlabelled checkpoint falls back to its filename with a visible warning
- [ ] The selected preset is written into the conversion record and is observable at the converter port