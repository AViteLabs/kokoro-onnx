# Changes

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
