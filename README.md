# redlnx-runtime-deps

Binaries that RedLnx downloads on demand. Nothing here is meant to be fetched by hand.

| Tag | Contents |
|---|---|
| `v1` | CUDA 12 and cuDNN 9, Windows x64 |
| `v1-windows-runtime` | ONNX Runtime 1.24.2, Windows x64: CUDA, DirectML, WebGPU |
| `v1-linux-runtime` | ONNX Runtime 1.24.2, Linux x64: WebGPU |
| `v1-linux-cuda` | ONNX Runtime 1.24.2, CUDA 12 and cuDNN 9, Linux x64 |
| `v1-models` | Model weights |
| `v1-camera-looks-f` | Camera Looks F v1 |

`manifest.json` lists every asset with its size and SHA-256, and the URL it was copied from. The app carries the same SHA-256 values and rejects a file that differs.

`.github/workflows/mirror-release.yml` copies the assets from that URL after checking size and SHA-256, then checks the anonymous download of the published release.

## Licenses

The RedLnx source is AGPL-3.0. The files here are not. ONNX Runtime is MIT. CUDA and cuDNN are NVIDIA's and redistributed under NVIDIA's license. Models carry their own licenses. Sources and terms are in [NOTICE](NOTICE).

RedLnx is not affiliated with NVIDIA or Microsoft.

Source: https://github.com/RedLnx-dev
