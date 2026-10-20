# 12: Run it on the GPU machine

**What to build:** Getting the app onto the 3070 Ti box with one command, and having it tell the truth about what it finds there. A single start script brings the app up; the app reports the device it detected and warns when that device is below the supported floor; missing ffmpeg or a missing converter environment is named explicitly, with conversions refused rather than failing obscurely; and the whole deploy is a `git pull` plus that script, with no build step and no second toolchain.

**Blocked by:** 02

**Status:** ready-for-agent

- [ ] On a machine with the repository cloned, one script starts the app and it is reachable on localhost
- [ ] The app reports the detected GPU and its capability, and warns when it is below the supported floor
- [ ] Missing ffmpeg produces an actionable message while still allowing the app to start and explain itself
- [ ] A missing or broken converter environment is reported explicitly, and conversions are refused up front rather than failing mid-pipeline
- [ ] Deploying an update requires only `git pull` and the start script — no client-side build step, no package manager beyond Python
- [ ] The stand-in converter can be selected explicitly, so the app runs end to end on a machine with no usable GPU