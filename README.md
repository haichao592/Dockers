

## Pull Built Images

Images are available in [DockerHub](https://hub.docker.com/u/hczhu/).

For example:
```
# Basic Pytorch runtime with minimum dependency, AMP enabled
docker pull hczhu/pytorch:pytorch1.5.1cu101-cuda10.1-cudnn7-py3.7-ubuntu18.04-runtime

# Selected libraries from Pytorch Ecosystem for NLP
docker pull hczhu/nlp:nlp0.3.0-transformers2.11.0-pl0.8.1-hydra1.0.0rc1-dgl0.4.3.post2
```
## Build Images
Build with default args:
```
git clone https://github.com/haichao592/dockers.git
cd dockers/pytorch
DOCKER_BUILDKIT=1 docker build -t nlp:latest .
```

Build a custom image by specifying the Docker build args:
```
#!/bin/bash

CUDA_VERSION=10.1
CUDNN_VERSION=7
PYTHON_VERSION=3.7
PYTORCH_VERSION=1.5.1+cu101

APEX_COMMIT=1f2aa9156547377a023932a1512752c392d9bbdf

TAG=hczhu/pytorch:pytorch${PYTORCH_VERSION}-cuda${CUDA_VERSION}-cudnn${CUDNN_VERSION}-py${PYTHON_VERSION}-ubuntu18.04-runtime
TAG=`echo $TAG | tr -d '+'`

DOCKER_BUILDKIT=1 docker build \
    -t $TAG \
    --build-arg CUDA_VERSION=${CUDA_VERSION} \
    --build-arg CUDNN_VERSION=${CUDNN_VERSION} \
    --build-arg PYTHON_VERSION=${PYTHON_VERSION} \
    --build-arg PYTORCH_VERSION=${PYTORCH_VERSION} \
    --build-arg APEX_COMMIT=${APEX_COMMIT} \
    --build-arg HYDRA_COMMIT=${HYDRA_COMMIT} .
```

## Run

```
docker run -it --rm --ipc=host \
  --name nlp_gpu \
  --user "$(id -u):$(id -g)" --userns host \ 
  --gpus '"device=2,3"' \
  --mount type=bind,source="$(pwd)",target=/workspace \
  --mount type=bind,source=$HOME/data,target=/workspace/data \
  pytorch:pytorch1.5.1-cuda10.1-cudnn7-py3.7-ubuntu18.04
```
Above command:
 - runs a container named **nlp_gpu** ready for Multi-GPU program
 - projects **local user** as a **non-root user** that works with Docker namespace for manipulating files
 - runs with GPU 2 and 3 (local rank), GPUP ranks in container starts from 0
 - mounts local **current directory** to **/workspace** in container
 - mounts local data directory **$HOME/data** to **/workspace/data** (since soft links in local machine cant not be accessed in container, so mount it)
