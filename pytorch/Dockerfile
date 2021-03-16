ARG CUDA_VERSION=10.1
ARG CUDNN_VERSION=7
FROM nvidia/cuda:${CUDA_VERSION}-cudnn${CUDNN_VERSION}-devel-ubuntu20.04 as build


RUN apt-get update && apt-get install -y --no-install-recommends \
         build-essential \
         cmake \
         git \
         curl \
         ca-certificates && \
     rm -rf /var/lib/apt/lists/*

# conda
ARG PYTHON_VERSION=3.6
RUN curl -o ~/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
     chmod +x ~/miniconda.sh && \
     ~/miniconda.sh -b -p /opt/conda && \
     rm ~/miniconda.sh && \
     /opt/conda/bin/conda install -y python=$PYTHON_VERSION && \
     /opt/conda/bin/conda clean -ya

ENV PATH /opt/conda/bin:$PATH

# pytorch
ARG PYTORCH_VERSION=1.7.1
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir torch==${PYTORCH_VERSION} -f https://download.pytorch.org/whl/torch_stable.html


# essential libs
RUN pip install --no-cache-dir tqdm tensorboard jupyterlab==2.2.5 ipython psutil matplotlib

ARG APEX_COMMIT=a78ccf0b3e3f7130b3f157732dc8e8e651389922
RUN git clone https://github.com/NVIDIA/apex.git apex && \
    cd apex && \
    git reset --hard ${APEX_COMMIT} && \
    pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" .

FROM nvidia/cuda:${CUDA_VERSION}-cudnn${CUDNN_VERSION}-runtime-ubuntu20.04

RUN apt-get update && apt-get install -y --no-install-recommends \
         build-essential \
         cmake \
         git \
         curl \
         vim \
         openssh-server \
         ca-certificates && \
     rm -rf /var/lib/apt/lists/*
     
COPY --from=build /opt/conda /opt/conda

ENV PATH /opt/conda/bin:$PATH

WORKDIR /workspace
CMD ["/bin/bash"]
