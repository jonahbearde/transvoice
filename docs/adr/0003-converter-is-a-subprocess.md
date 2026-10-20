# The converter runs as a subprocess in its own environment

Status: accepted

Voice conversion is invoked as a child process running RVC's offline CLI, never imported into the application. RVC's inference stack is importable and Gradio-free, but importing it requires changing the working directory to RVC's project root, setting four path environment variables, and surrendering to a singleton configuration object that sniffs the GPU at import time — and its pinned dependencies (torch 2.7.1, numpy < 2) collide with the application's. The child process pays one spawn per chunk and buys total isolation.

## Consequences

- The application never shares a Python environment with the converter, so the app is free to pin modern dependencies while RVC keeps its own.
- The subprocess boundary is the substitution point that makes the whole pipeline testable on a machine without a usable GPU: a stand-in converter that genuinely transforms audio can be bound in its place. This is not test scaffolding to be deleted later — it is also how the tool degrades on hardware below the supported floor.
- Failures arrive as exit codes and stderr text rather than exceptions, so the converter port must translate them into failure kinds the pipeline can act on (bad preset, out of memory, crash).
- Per-chunk spawning costs model load time on every chunk. If that becomes the dominant cost on long conversions, the correct response is a resident worker process behind the same port — not importing the model in-process.