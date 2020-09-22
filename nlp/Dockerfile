FROM hczhu/pytorch:pytorch1.6.0cu101-cuda10.1-cudnn7-py3.7-ubuntu18.04-runtime

ARG TRANSFORMERS=3.1.0
ARG DATASETS=1.0.2
ARG LIGHTNING=0.9.0
ARG HYDRA=1.0.2

RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir --upgrade transformers==${TRANSFORMERS} \
                                         datasets==${DATASETS} \
                                         pytorch-lightning==${LIGHTNING} \
                                         hydra-core==${HYDRA} && \
    pip install --no-cache-dir --upgrade hydra-nevergrad-sweeper --pre


WORKDIR /workspace
CMD ["/bin/bash"]
