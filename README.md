# sem5-nlp-labs

## Environment setup (one venv for all sessions)

This repo uses **one** virtual environment (`.venv/` at the repo root) for every
session's notebooks. New sessions never need a new venv or a new kernel —
only a new line in `requirements.txt`.

### The concepts, briefly

- **Virtual environment (venv)** — a self-contained folder (`.venv/`)
  holding a Python interpreter plus whatever packages get installed into it,
  isolated from other projects on your machine.
- **Jupyter kernel** — the running Python process a notebook talks to when
  you run a cell. The `ipykernel` package (installed in `.venv`) is what lets
  a Python interpreter act as one.
- **Two ways VS Code can find that kernel:**
  - **Python Environments** — VS Code detects `.venv\Scripts\python.exe`
    inside the project and starts a kernel from it directly. Nothing to
    register; it lives entirely in the repo. **Use this one.**
  - **Jupyter Kernel** — VS Code reads a registered `kernel.json` stored
    outside the repo in `%APPDATA%\jupyter\kernels\`. It can go stale if the
    repo moves, so avoid it here.

### Selecting the kernel in a notebook

Select Kernel (top right) -> **Python Environments...** ->
**`.venv (Python 3.12.x)  .venv\Scripts\python.exe`** (the one with the
relative path).

### Adding a new package for a new session

1. Add the line to the root `requirements.txt`, e.g. `gensim==4.3.3`.
   If the package is already listed at the same version, a duplicate line is
   harmless. If the version differs, edit the existing line instead — two
   conflicting versions make the install fail (loudly, naming the package).
2. From the repo root, run:
   ```
   uv pip install -r requirements.txt
   ```
   This installs only what's new/changed; satisfied packages are skipped.
3. In the open notebook, restart the kernel (toolbar restart icon). Don't
   reselect anything — same `.venv`, now with the new package importable.

### If VS Code doesn't show the `.venv` environment

Command Palette -> "Developer: Reload Window", then try Select Kernel again.
