

# Pre-built Wheels for llama-cpp-python

<div align="center">
<a href="https://colab.research.google.com/drive/1OUVAO8T_HaYW0zxYDkzGja-2sD3elhJp"><img src="https://img.shields.io/static/v1?message=Open%20in%20Colab&logo=googlecolab&labelColor=5c5c5c&color=0f80c1&label=%20" alt="Open in Colab"></a>
</div>

Pre-built wheels for [llama-cpp-python](https://github.com/abetlen/llama-cpp-python)  
To install the package, copy the wheel file's URL from the [Releases](https://github.com/sergey21000/llama-cpp-python-wheels/releases) page and run:
```sh
pip install PASTE_THE_COPIED_URL_HERE
```

# Installation Examples

> [!NOTE]
> If `import llama_cpp` returns an error `Failed to load shared library: libgomp.so.1`, then you need to install the library
> ```sh
> sudo apt-get update && apt-get install -y libgomp1
> ```

Linux x86_64 / Python 3.11 / CPU 
```sh
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.15-cpu/llama_cpp_python-0.3.15-cp311-cp311-linux_x86_64.whl
```

Linux x86_64 / Python 3.11 / CUDA 12.4 
```sh
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.15-cu124/llama_cpp_python-0.3.15-cp311-cp311-linux_x86_64.whl
```

Linux x86_64 / Python 3.12 / CPU (Google Colab)
```sh
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.15-cpu/llama_cpp_python-0.3.15-cp312-cp312-linux_x86_64.whl
```

Linux x86_64 / Python 3.12 / CUDA 12.4 (Google Colab)
```sh
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.15-cu124/llama_cpp_python-0.3.15-cp312-cp312-linux_x86_64.whl
```

Windows amd64 / Python 3.12 / CPU
```powershell
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.15-cpu/llama_cpp_python-0.3.15-cp312-cp312-win_amd64.whl
```

Windows amd64 / Python 3.12 / CUDA 12.8
```powershell
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/v0.3.15-cu128-win/llama_cpp_python-0.3.15-cp312-cp312-win_amd64.whl
```


# Build Instructions

## Example: Building llama-cpp-python with CUDA support in Google Colab

1) Build the latest version of `llama-cpp-python` with CUDA support into the `wheel_dir` directory
```sh
!CMAKE_ARGS="-DGGML_CUDA=on" pip wheel --no-deps --wheel-dir=wheel_dir llama-cpp-python
```
The build process takes about 30–40 minutes. Make sure that a GPU is enabled in your Colab environment.  
Once completed, the `.whl` file will be located in the `wheel_dir` directory.  
The `.whl` file will be compiled for the architecture of the current GPU, if you need to compile with support for other CUDA architectures, you need to specify
```sh
!CMAKE_ARGS="-DGGML_CUDA=on -DCMAKE_CUDA_ARCHITECTURES=75;80;86;89;90" pip wheel --no-deps --wheel-dir=wheel_dir llama-cpp-python
```

2) (Optional) Saving the `.whl` file to Google Drive for convenience (after mounting the drive)
```python
import shutil
src_wheel_file = 'wheel_dir/llama_cpp_python-0.3.14-cp311-cp311-linux_x86_64.whl'
trg_wheel_file = '/content/drive/MyDrive/llama_cpp_python-0.3.14-cp311-cp311-linux_x86_64.whl'
shutil.copyfile(src_wheel_file, trg_wheel_file)
```

3) Installing from a saved wheel:
```sh
!pip install wheel_dir/llama_cpp_python-0.3.14-cp311-cp311-linux_x86_64.whl
```


## Example: Building llama-cpp-python on Windows with CUDA support

Build the latest version of `llama-cpp-python` with CUDA support into the `wheel_dir` directory (Windows Powershell)
```powershell
$env:FORCE_CMAKE='1'; $env:CMAKE_ARGS='-DGGML_CUDA=on'
pip wheel --no-deps --no-cache-dir --wheel-dir=wheel_dir llama-cpp-python
```

If `DLLAMA_AVX` or other instructions are not supported then you need to specify this
```powershell
$env:FORCE_CMAKE='1'; $env:CMAKE_ARGS='-DGGML_CUDA=on -DLLAMA_AVX=off -DLLAMA_AVX2=off -DLLAMA_FMA=off'
pip wheel --no-deps --no-cache-dir --wheel-dir=wheel_dir llama-cpp-python
```

Build for other CUDA architectures
```powershell
$env:FORCE_CMAKE='1'; $env:CMAKE_ARGS='-DGGML_CUDA=on -DCMAKE_CUDA_ARCHITECTURES=75;80;86;89;90'
pip wheel --no-deps --no-cache-dir --wheel-dir=wheel_dir llama-cpp-python
```

Instead of `pip wheel` you can use `pip install` to install the library right away

> [!NOTE]
> To install `llama-cpp-python` on Windows with CUDA support, you must first install [Visual Studio 2022 Community](https://visualstudio.microsoft.com/ru/downloads/) and [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive), as indicated in [this](https://github.com/abetlen/llama-cpp-python/discussions/871#discussion-5812096) or [this](https://github.com/Granddyser/windows-llama-cpp-python-cuda-guide?tab=readme-ov-file#12-visual-studio-2019-installation-and-configuration) instructions


## Example: Building llama-cpp-python on Android

Build the latest version of `llama-cpp-python` on Termux (Android, aarch64), taken from this [comment](https://github.com/abetlen/llama-cpp-python/issues/389#issuecomment-1913374996)
```sh
pkg update && pkg upgrade 
pkg install libexpat openssl python-pip python-cryptography cmake ninja autoconf automake libandroid-execinfo patchelf

# command for build wheels
pip wheel --no-deps --no-cache-dir --wheel-dir=wheel_dir llama-cpp-python
# or command to install
pip install llama-cpp-python
```
