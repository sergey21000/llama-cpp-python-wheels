

# Pre-built Wheels for llama-cpp-python

<div align="center">
<a href="https://colab.research.google.com/drive/1OUVAO8T_HaYW0zxYDkzGja-2sD3elhJp"><img src="https://img.shields.io/static/v1?message=Open%20in%20Colab&logo=googlecolab&labelColor=5c5c5c&color=0f80c1&label=%20" alt="Open in Colab"></a>
</div>

Pre-built wheels for [llama-cpp-python](https://github.com/abetlen/llama-cpp-python) which were built on the following OS:
- Linux x86_64 (Ubuntu 22.04) / Python 3.11 / CPU / CUDA (12.5) (Google Colab)
- Linux aarch64 (Ubuntu 22.04) / Python 3.10 (Android)
- Linux aarch64 (Termux) / Python 3.12 (Android)
- Windows 10 / Python 3.12 / CPU / CUDA (12.8)

All available wheels can be found in the [Releases](https://github.com/sergey21000/llama-cpp-python-wheels/releases)


# Installation Examples

Linux x86_64 / Python 3.11 / CPU (Google Colab)
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.14/llama_cpp_python-0.3.14-cp311-cp311-linux_x86_64.cpu.whl
```

Linux x86_64 / Python 3.11 / CUDA (Google Colab)
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.14/llama_cpp_python-0.3.14-cp311-cp311-linux_x86_64.cuda.whl
```

Windows amd64 / Python 3.12 / CPU
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.14/llama_cpp_python-0.3.14-cp312-cp312-win_amd64.cpu.whl
```

Windows amd64 / Python 3.12 / CUDA
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.14/llama_cpp_python-0.3.14-cp312-cp312-win_amd64.cuda.whl
```

Linux aarch64 / Python 3.10 (Android, Ubuntu 22.04)
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.14/llama_cpp_python-0.3.14-cp310-cp310-linux_aarch64.whl
```

Linux aarch64 / Python 3.12 (Android, Termux)
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.14/llama_cpp_python-0.3.14-cp312-cp312-linux_aarch64.whl
```


# Build Instructions

## Example: Building llama-cpp-python with CUDA support in Google Colab

1) Build the latest version of `llama-cpp-python` with CUDA support into the `wheel_dir` directory
```
!CMAKE_ARGS="-DGGML_CUDA=on" pip wheel --no-deps --wheel-dir=wheel_dir llama-cpp-python
```
The build process takes about 30–40 minutes. Make sure that a GPU is enabled in your Colab environment.  
Once completed, the `.whl` file will be located in the `wheel_dir` directory.

2) (Optional) Saving the `.whl` file to Google Drive for convenience (after mounting the drive)
```python
import shutil

src_wheel_file = 'wheel_dir/llama_cpp_python-0.3.14-cp311-cp311-linux_x86_64.whl'
trg_wheel_file = '/content/drive/MyDrive/llama_cpp_python-0.3.14-cp311-cp311-linux_x86_64.whl'
shutil.copyfile(src_wheel_file, trg_wheel_file)
```

3) Installing from a saved wheel:
```
!pip install wheel_dir/llama_cpp_python-0.3.14-cp311-cp311-linux_x86_64.whl
```


## Example: Building llama-cpp-python on Windows with CUDA support

Build the latest version of `llama-cpp-python` with CUDA support into the `wheel_dir` directory (Windows Powershell)
```
$env:FORCE_CMAKE='1'; $env:CMAKE_ARGS='-DGGML_CUDA=on'
pip wheel --no-deps --no-cache-dir --wheel-dir=wheel_dir llama-cpp-python
```

If `DLLAMA_AVX` or other instructions are not supported then you need to specify this
```
$env:FORCE_CMAKE='1'; $env:CMAKE_ARGS='-DGGML_CUDA=on -DLLAMA_AVX=off -DLLAMA_AVX2=off -DLLAMA_FMA=off'
pip wheel --no-deps --no-cache-dir --wheel-dir=wheel_dir llama-cpp-python
```

> [!NOTE]
> To install `llama-cpp-python` on Windows with CUDA support, you must first install [Visual Studio 2022 Community](https://visualstudio.microsoft.com/ru/downloads/) and [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive), as indicated in [this](https://github.com/abetlen/llama-cpp-python/discussions/871#discussion-5812096) or [this](https://github.com/Granddyser/windows-llama-cpp-python-cuda-guide?tab=readme-ov-file#12-visual-studio-2019-installation-and-configuration) instructions


## Example: Building llama-cpp-python on Android

Build the latest version of `llama-cpp-python` on Termux (Android, aarch64)
```
pkg update && pkg upgrade 
pkg install libexpat openssl python-pip python-cryptography cmake ninja autoconf automake libandroid-execinfo patchelf
pip wheel --no-deps --no-cache-dir --wheel-dir=wheel_dir llama-cpp-python
```

Source:  
https://github.com/abetlen/llama-cpp-python/issues/389#issuecomment-1913374996
