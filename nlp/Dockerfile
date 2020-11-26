ARG BASE
FROM ${BASE}

ARG TRANSFORMERS
ARG DATASETS
ARG LIGHTNING
ARG HYDRA
ARG FAISS

RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir --upgrade transformers==${TRANSFORMERS} \
                                         datasets==${DATASETS} \
                                         pytorch-lightning==${LIGHTNING} \
                                         hydra-core==${HYDRA} \
                                         optuna && \
    pip install --no-cache-dir --upgrade hydra-nevergrad-sweeper --pre && \
    conda install -c pytorch faiss-gpu==${FAISS} cudatoolkit=10.1 && \
    conda clean -ya


WORKDIR /workspace
CMD ["/bin/bash"]
