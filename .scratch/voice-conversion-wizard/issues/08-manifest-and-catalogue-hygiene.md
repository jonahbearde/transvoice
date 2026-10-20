# 08: Manifest, setup fetch, and catalogue hygiene

**What to build:** A first-run experience where the wizard is not empty, without shipping voice weights in the repository. A shipped manifest lists remotely hosted presets with their labels and timbre tags; an explicit setup command fetches them into the catalogue. The catalogue view reports each preset's disk usage and the total, presets can be removed without breaking the listing, and a label containing a delivery adjective is refused at import with an explanation, because the tool cannot deliver on that promise.

**Blocked by:** 03

**Status:** ready-for-agent

- [ ] Running setup fetches the manifest's presets into the catalogue, labelled and tagged, so the picker is populated on a fresh clone
- [ ] The repository contains no voice weights; the manifest is the only shipped reference to them
- [ ] The catalogue view reports per-preset and total disk usage
- [ ] Removing a preset deletes its files and drops it from the picker without restarting
- [ ] Importing a preset labelled with a delivery adjective is refused with a message explaining that delivery is inherited from the narrator
- [ ] Importing a preset labelled with timbre words only is accepted
- [ ] A failed or offline setup produces an actionable message rather than an empty catalogue with no explanation