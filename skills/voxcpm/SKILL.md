---
name: voxcpm
description: Set up and use the VoxCPM CLI for local text-to-speech, voice design, and reference-audio voice cloning. Use whenever the user asks to run VoxCPM or VoxCPM2 from the terminal, generate speech with VoxCPM, clone a voice with VoxCPM, or troubleshoot its CLI installation or generation. This skill covers CLI workflows only, not the Python API, web demo, unrelated TTS engines, or general audio editing.
---

# VoxCPM CLI

## Scope and workflow

Use the `voxcpm` command for all speech generation. Do not introduce Python scripts, API examples, or the web demo. Use `openbmb/VoxCPM2`, the current CLI default, unless the user requires another checkpoint.

Inspect the existing environment before changing dependencies. Ask only for missing decisions: text to speak, output path, and reference audio if cloning is wanted. When guiding the user interactively, give one actionable step and wait for their result before continuing.

Do not install packages or download model weights merely to explain usage. Before a first generation, explain that weights download automatically and require several GB of disk space. Use voice samples the user owns or has permission to use.

## Install and check the CLI

The documentation recommends Python 3.10–3.12 (3.10–3.11 most tested) and PyTorch 2.5.0 or newer. CUDA is optional; the documented NVIDIA requirement is CUDA 12.0 or newer. Do not replace an existing PyTorch installation blindly.

Prefer the project's existing environment. For a new environment, use the standard-library route without requiring `uv`:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install voxcpm
voxcpm --help
```

These commands are a reference sequence; present them individually during interactive setup. If `.venv` exists, inspect and reuse it instead of recreating it. If `venv` or `pip` is missing, report that blocker and ask before installing system packages. If `uv` is missing, use this route rather than running an unsolicited installer. In an existing uv-managed project, follow its dependency workflow instead.

Check the installed command surface before using extra options:

```bash
voxcpm design --help
voxcpm clone --help
python -m pip show voxcpm
```

Treat installed help as authoritative for available flags. Do not translate Python parameter names into guessed CLI flags or silently upgrade when commands differ from current documentation. A successful help command verifies CLI availability, not model loading or audio generation.

## Generate speech and design a voice

```bash
voxcpm design --text "Hello from VoxCPM! Welcome to this example." --output out.wav
```

For voice design, prepend a parenthesized English or Chinese instruction:

```bash
voxcpm design --text "(A warm, calm narrator)Welcome to today's story." --output narration.wav
```

Without reference audio, timbre can vary between calls. Do not promise a consistent speaker from a voice description alone. Quote text and paths safely for the active shell; do not interpolate untrusted text into executable shell syntax. Check before overwriting an existing output file.

## Clone a voice

VoxCPM 2 supports reference-only cloning without a transcript:

```bash
voxcpm clone --text "Welcome back! It is good to hear from you." --reference-audio speaker.wav --output cloned.wav
```

Prefer clean reference audio, practically 5–30 seconds long. Reuse the same reference for consistent timbre. Verify the reference path exists before running generation.

For a noisy reference, optionally add `--denoise`:

```bash
voxcpm clone --text "This is a cloned voice sample." --reference-audio speaker.wav --output cloned.wav --denoise
```

Denoising processes reference audio, not generated output. Its 16 kHz pipeline can alter voice characteristics; omit it for clean audio or if similarity worsens.

For transcript-conditioned cloning or older checkpoints, consult `voxcpm clone --help` and the version-specific documentation first. Do not invent flags or transcripts. VoxCPM 1.x does not support the same reference-only workflow as VoxCPM 2.

## Select a device

Automatic selection prefers CUDA, then MPS, then CPU. Explicit requests fail if the selected backend is unavailable rather than silently falling back.

CPU fallback with compilation disabled:

```bash
voxcpm design --text "Hello from the CPU! This is a test sample." --device cpu --no-optimize --output cpu.wav
```

Apple Silicon MPS:

```bash
voxcpm design --text "Hello from VoxCPM on Apple Silicon." --device mps --no-optimize --output mps.wav
```

Use `--no-optimize` when compilation causes compatibility problems. Check subcommand help before overriding the checkpoint with `--hf-model-id` or adding tuning options.

## Troubleshoot

| Symptom | Action |
| --- | --- |
| `voxcpm: command not found` | Check environment activation and installation in that environment. |
| Unknown command or flag | Inspect installed help and package version; do not guess a replacement. |
| Backend or compilation error | Check device availability; try `--device cpu --no-optimize`. |
| Weak output from a single short word | Try a natural sentence lasting a few seconds. |
| Inconsistent speaker | Reuse a reference with `voxcpm clone`. |
| Poor cloning similarity | Use a cleaner reference; compare with denoising disabled. |
| Buzzing, runaway generation, or out-of-memory on long text | Split text at sentence or paragraph boundaries and generate separate WAV files, reusing the reference. |
| Numbers/dates spoken awkwardly | Spell them out or inspect help for a supported normalization option. |
| Download failure | Check connectivity, disk space, and the actual error before retrying. |

For quality tuning, normalization, file-based text input, or streaming, first inspect installed help. Use only supported CLI features; if a feature is not exposed, state the limitation instead of switching to the Python API. Joining generated audio is outside this skill's scope unless requested.

Do not redirect downloads through a third-party mirror without user approval. The installation docs describe `HF_ENDPOINT` for that optional setup.

## Verify and report

After an authorized generation, confirm the output exists and is nonempty. If an audio inspection tool such as `ffprobe` is available, verify it is readable audio with a positive duration. Listen if playback tools are available; otherwise state that sound quality was not checked.

Report the output path, command used, and checks actually performed. Do not claim a successful help command proves usable speech. Do not install additional inspection or playback tools without approval.

## Official references

Consult relevant documentation when installed help is insufficient; `latest` can change:

- [Quick Start](https://voxcpm.readthedocs.io/en/latest/quickstart.html)
- [Installation](https://voxcpm.readthedocs.io/en/latest/installation.html)
- [Usage Guide](https://voxcpm.readthedocs.io/en/latest/usage_guide.html)
- [FAQ and troubleshooting](https://voxcpm.readthedocs.io/en/latest/faq.html)
