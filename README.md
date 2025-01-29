# ML Development Container with CUDA, PyEnv, and Hugging Face Tools

GPU-ready ML development container.

Download from Docker Hub: [ivanvmoreno/ml-dev-pod](https://hub.docker.com/r/ivanvmoreno/ml-dev-pod)

## 🚀 Core Components

1. **Base Image**
   ```dockerfile
   FROM nvidia/cuda:12.3.2-cudnn9-devel-ubuntu22.04
   ```
   - **Why**: Provides full CUDA 12.3 + cuDNN 9 stack for GPU acceleration
   - **Benefit**: Native support for modern ML frameworks (PyTorch/TensorFlow)

2. **Environment Variables**
   ```dockerfile
   ENV HF_HOME="/runpod-volume/.cache/huggingface/"
   ENV PIP_CACHE_DIR="/runpod-volume/.cache/pip"
   ENV PYENV_ROOT="$HOME/.pyenv"
   ```
   - **Why**: Centralized cache management and Python version control
   - **Benefit**: Persistent caches when using volumes, isolated Python environments

## 📦 Key Package Groups

1. **System Essentials**
   ```dockerfile
   git-lfs openssh-server nvtop task-spooler
   ```
   - **Why**: Large file support, SSH access, GPU monitoring
   - **Benefit**: Full dev environment with debugging tools

2. **ML Dependencies**
   ```dockerfile
   libblas-dev liblapack-dev libhdf5-serial-dev
   ```
   - **Why**: Optimized linear algebra and HDF5 support
   - **Benefit**: Required for NumPy/PyTorch performance

3. **Storage Support**
   ```dockerfile
   cifs-utils nfs-common zstd
   ```
   - **Why**: Network filesystem protocols + compression
   - **Benefit**: Cloud storage integration

## 🐍 Python Environment

1. **PyEnv Installation**
   ```dockerfile
   RUN curl https://pyenv.run | bash
   ```
   - **Why**: Multi-Python version management
   - **Benefit**: Isolated Python 3.11 environment without system conflicts

2. **Pip Configuration**
   ```dockerfile
   PIP_PREFER_BINARY=1 PYTHONUNBUFFERED=1
   ```
   - **Why**: Stable binaries and real-time logging
   - **Benefit**: Faster installs with precompiled wheels

## 🤖 ML Ecosystem Tools

1. **Hugging Face Stack**
   ```dockerfile
   pip install -U "huggingface_hub[cli]"
   ```
   - **Benefit**: Easy model/dataset uploads/downloads from Hub

2. **ZSH Terminal**
   ```dockerfile
   RUN sh -c "$(curl -L ...zsh-in-docker.sh)"
   ```
   - **Why**: Modern shell with plugins
   - **Benefit**: Improved productivity with autocomplete