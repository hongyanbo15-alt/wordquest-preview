# Third-party notices

## Word recognition model and image preprocessing

WordQuest uses the AccuScan int8 word recognition model and adapts its image preprocessing TypeScript implementation:

- Author / copyright: Copyright (c) 2026 Shashank Yadav.
- Repository: https://github.com/shashank11yadav/AccuScan
- Pinned commit: `faf7bdf130f70165234911d40dde5aa37e503ce0`.
- Model source: `web/public/models/model.onnx`, redistributed as `public/models/words/model.onnx`.
- Preprocessing source: `web/src/ml/preprocess.ts`, adapted as `src/lib/handwriting/wordPreprocess.ts` with attribution.
- License: MIT, reproduced verbatim in `public/models/words/LICENSE`.
- Model provenance, size and SHA-256: `public/models/words/provenance.json`.

The upstream project documents GNHK (GoodNotes, CC BY 4.0), OFL handwriting fonts and public-domain training text in its README. WordQuest redistributes the model, not those datasets or fonts. WordQuest does not include AccuScan's dictionary or language-model decoding. It performs greedy CTC decoding independently of lesson answers.

## ONNX Runtime Web

The word model runs locally in a Web Worker with `onnxruntime-web` 1.30.0, using the single-threaded WebAssembly execution provider. The MIT license is distributed in `public/licenses/onnxruntime-LICENSE`.

Project: https://github.com/microsoft/onnxruntime

Only the plain WASM runtime is included in the production output; no WebGPU, JSEP, JSPI or asyncify runtime is needed. All runtime and model assets are served from the website's own origin. No handwriting is sent to an external recognition service.

## Letter recognition model

The letter-only, float16 TensorFlow.js model in `public/models/letters/` is redistributed from:

- Project: Handwriting Recognition in VR
- Author / copyright: Copyright (c) 2023 Akbar S.
- Repository: https://github.com/akbartus/Handwriting-Recognition-in-VR
- Commit: `e00a35c0e4bd3d797febdc7853675634e463da54`
- Source directory: `serveless/misc/model_fp16/`
- License: MIT, reproduced verbatim in `public/models/letters/LICENSE`.
- File paths, sizes and SHA-256 checksums: `public/models/letters/provenance.json`.

WordQuest uses these model files with its own stroke capture, letter grouping and spelling flow. It does not include the upstream dictionary, Google IME integration, OpenCV.js, or VR implementation.

## TensorFlow.js

The runtime uses `@tensorflow/tfjs-core`, `@tensorflow/tfjs-layers`, and `@tensorflow/tfjs-backend-cpu`, under the Apache License 2.0. See the license included in these installed packages and the distributed copy in `public/licenses/tensorflowjs-LICENSE`.

Project: https://github.com/tensorflow/tfjs

The dependency lockfile records the exact runtime versions. The handwriting engine is loaded only when the learner requests recognition; handwriting data is processed locally in the browser.
