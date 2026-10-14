RedLnx Runtime Dependencies — Linux x86_64, ONNX Runtime CUDA
=============================================================

This release contains pre-built binary shared objects from NVIDIA
Corporation, redistributed under the terms of the NVIDIA Software License
Agreement, and the official Microsoft ONNX Runtime Linux GPU build.  The
NVIDIA files are NOT open-source and are NOT covered by the AGPL-3.0
license that governs the RedLnx source code.

The included libraries are unmodified copies of the official redistributable
binaries obtained from:

  ONNX Runtime  — https://github.com/microsoft/onnxruntime/releases/tag/v1.24.2
                  onnxruntime-linux-x64-gpu-1.24.2.tgz
  CUDA Toolkit  — https://developer.download.nvidia.com/compute/cuda/redist
                  (redistrib_12.8.1.json)
  cuDNN SDK     — https://developer.download.nvidia.com/compute/cudnn/redist
                  (redistrib_9.21.1.json)

By downloading or using these files you agree to the license terms included
in the packages:

  LICENSE                   — ONNX Runtime (MIT), in the onnxruntime archive
  ThirdPartyNotices.txt     — ONNX Runtime third-party notices
  NVIDIA-CUDA-LICENSE.txt   — NVIDIA CUDA Toolkit EULA, in the cuda12 archive
  NVIDIA-CUDNN-LICENSE.txt  — NVIDIA cuDNN SDK License Agreement, in the cudnn9 archive

NVIDIA, CUDA and cuDNN are trademarks or registered trademarks of NVIDIA
Corporation.  This redistribution is permitted under section 1.1(iii) and 1.2
of the NVIDIA Software License Agreement, which allows distribution of the
"distributable" portions of the SDK as incorporated into a software
application with material additional functionality.

RedLnx is not affiliated with, endorsed by, or sponsored by NVIDIA
Corporation or Microsoft Corporation.

Why three archives
------------------
The split is deliberate: a user on ROCm, Vulkan or CPU must not download
750 MB of CUDA libraries to get an ONNX Runtime.  Each archive is fetched
only when the runtime that needs it is installed.

Package contents
----------------
redlnx-onnxruntime-linux-x64-cuda-1.24.2.tar.zst   (155 MiB)
  libonnxruntime.so{,.1,.1.24.2}
  libonnxruntime_providers_shared.so
  libonnxruntime_providers_cuda.so
  LICENSE, ThirdPartyNotices.txt, VERSION_NUMBER

redlnx-cuda12-linux-x64.tar.zst                    (759 MiB)
  libcudart.so.12      (12.8.90)
  libcublas.so.12      (12.8.4.1)
  libcublasLt.so.12    (12.8.4.1)
  libcufft.so.11       (11.3.3.83)
  libcurand.so.10      (10.3.9.90)
  libnvrtc.so.12       (12.8.93)
  libnvrtc-builtins.so.12.8 (12.8.93)
  NVIDIA-CUDA-LICENSE.txt

redlnx-cudnn9-cuda12-linux-x64.tar.zst             (584 MiB)
  libcudnn.so.9 and the eight cuDNN 9.21.1.3 engine/dispatch libraries
  NVIDIA-CUDNN-LICENSE.txt

What is deliberately NOT here
-----------------------------
libonnxruntime_providers_tensorrt.so — TensorRT itself is not redistributed,
  so shipping a provider that can never load would only create a silent
  degradation path.
libcusparse, libnvblas, libcufftw, the link-time stubs/ directories and the
  static .a archives — none of them appear in the dynamic dependencies of
  libonnxruntime_providers_cuda.so, verified with readelf on the pinned build.

Compatibility
-------------
ONNX Runtime 1.24.2, CUDA 12 Execution Provider.  The CUDA sonames the
provider actually requires, read from the binary and not assumed:
libcublasLt.so.12, libcublas.so.12, libcurand.so.10, libcufft.so.11,
libcudart.so.12, libcudnn.so.9.  Note the cuFFT major: 11, the CUDA 12
family — the same pin the Windows bundle carries as cufft64_11.dll.
libnvrtc is not a link-time dependency: cuDNN dlopens it for the
runtime-compiled engines, and omitting it would disable them silently.

The host still provides the NVIDIA kernel driver and libcuda.so.1; only the
user-space CUDA runtime is shipped here.

