# Changes

## 0.7.2 (2026-10-05)

- Drop the `cffi` and `lxml` dependencies: nothing in the dependency tree
  needs them. They were only direct pins to force Python 3.14-compatible
  versions of the old `phonemizer-fork` transitive stack, which 0.7.1
  removed. This also avoids constraining `lxml` for consumers that pin
  older versions.

## 0.7.1 (2026-10-05)

- Switch `phonemizer-fork` to stock `phonemizer>=3.4.0`, matching upstream.
  Stock 3.4.0 upstreamed the fork's `set_data_path` support and ships a
  bounded backend cache; output is byte-identical for our usage. This
  also drops the `segments`/`csvw`/`rdflib` pins and
  `constraints-py314.txt`, which only existed for the fork's transitive
  stack. Consumers that still pull `phonemizer-fork` via `misaki[en]`
  must exclude it at resolve time — the two packages provide the same
  `phonemizer` module.

## 0.7.0 (2026-10-05)

- Merge upstream `thewh1teagle/kokoro-onnx` 0.6.1:
  - chunked and continuous synthesis with timestamps
    (`chunker`, `sliding`, `session`, `pauses` modules)
  - pause placement fixes and weight-norm checkpoint repair
  - model downloads now point at `model-files-v1.1` (fp16 and int8
    variants alongside fp32)
- Keep `phonemizer-fork` instead of following upstream's switch to stock
  `phonemizer`: both packages provide the `phonemizer` module and cannot
  coexist, and consumers already depend on the fork. Pin
  `segments>=2.4.0`, `csvw>=4.1.0`, and `rdflib>=7.6.0` to keep its
  transitive stack Python 3.14-compatible.
- Switch the build backend from hatchling to `uv_build>=0.12.23,<0.13`.
- Raise dependency floors: `onnxruntime>=1.30.0`,
  `onnxruntime-gpu>=1.30.0`, `cffi>=2.1.1`, `lxml>=6.1.3`,
  `numpy>=2.5.3`; dev deps `ruff>=0.16.3`, `sounddevice>=0.5.6`,
  `soundfile>=0.14.0`.
- Widen the `gpu` extra marker to all of Linux: `onnxruntime-gpu` 1.30.0
  ships Linux aarch64 wheels (still unavailable on macOS).
- Python support remains `>=3.12,<3.15`; upstream still caps at `<3.14`.
