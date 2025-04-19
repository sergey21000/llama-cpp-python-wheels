# Pre-built Wheels for llama-cpp-python

Pre-built wheels for llama-cpp-python are available for the following OS and Python versions:
- Linux (Ubuntu 22.04) / Python 3.10 / CPU
- Linux (Ubuntu 22.04) / Python 3.11 / CPU
- Linux (Ubuntu 22.04) / Python 3.11 / CUDA
- Windows / Python 3.12 / CPU
- Windows / Python 3.12 / CUDA

All available wheels can be found in the [Releases](https://github.com/sergey21000/llama-cpp-python-wheels/releases)


# Installation Examples

Linux (Ubuntu 22.04) / Python 3.10 / CPU
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/llama-cpp-python-0.3.8-wheels/llama_cpp_python-0.3.8-cp310-cp310-linux_x86_64.cpu.whl
```

Linux (Ubuntu 22.04) / Python 3.11 / CPU (Google Colab)
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/llama-cpp-python-0.3.8-wheels/llama_cpp_python-0.3.8-cp311-cp311-linux_x86_64.cpu.whl
```

Linux (Ubuntu 22.04) / Python 3.11 / CUDA (Google Colab)
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/llama-cpp-python-0.3.8-wheels/llama_cpp_python-0.3.8-cp311-cp311-linux_x86_64.cuda.whl
```

Windows / Python 3.12 / CPU
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/llama-cpp-python-0.3.8-wheels/llama_cpp_python-0.3.8-cp312-cp312-win_amd64.cpu.whl
```

Windows / Python 3.12 / CUDA
```
pip install https://github.com/sergey21000/llama-cpp-python-wheels/releases/download/llama-cpp-python-0.3.8-wheels/llama_cpp_python-0.3.8-cp312-cp312-win_amd64.cuda.whl
```


# Build Instructions

Example: Building llama-cpp-python with CUDA support in Google Colab

1) To build the latest version of `llama-cpp-python` with CUDA support into the `llamacpp_wheel` directory:
```
!CMAKE_ARGS="-DGGML_CUDA=on" pip wheel --no-deps --wheel-dir=llamacpp_wheel llama-cpp-python
```
The build process takes about 30–40 minutes. Make sure that a GPU is enabled in your Colab environment.  
Once completed, the .whl file will be located in the llamacpp_wheel directory.

2) (Optional) Saving the `.whl` file to Google Drive for convenience (after mounting the drive)
```python
import shutil

src_wheel_file = 'llamacpp_wheel/llama_cpp_python-0.3.8-cp311-cp311-linux_x86_64.whl'
trg_wheel_file = '/content/drive/MyDrive/llama_cpp_python-0.3.8-cp311-cp311-linux_x86_64.whl'
shutil.copyfile(src_wheel_file, trg_wheel_file)
```

3) Installing from a saved wheel:
```
!pip install llamacpp_wheel/llama_cpp_python-0.3.8-cp311-cp311-linux_x86_64.whl
```

