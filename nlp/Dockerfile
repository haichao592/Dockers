ARG BASE
FROM ${BASE}

RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir --upgrade transformers \
                                         datasets \
                                         pytorch-lightning \
                                         hydra-core \
                                         comet-ml \
                                         optuna && \
    pip install --no-cache-dir --upgrade hydra-nevergrad-sweeper hydra-joblib-launcher --pre && \
    conda install -c pytorch faiss-gpu cudatoolkit=10.1 && \
    conda install -c dglteam dgl-cuda10.1 && \
    conda clean -ya


WORKDIR /workspace
CMD ["/bin/bash"]
