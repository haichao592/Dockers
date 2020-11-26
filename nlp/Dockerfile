ARG BASE
FROM ${BASE}

RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir --upgrade transformers \
                                         datasets \
                                         pytorch-lightning \
                                         hydra-core \
                                         optuna && \
    pip install --no-cache-dir --upgrade hydra-nevergrad-sweeper --pre && \
    conda install -c pytorch faiss-gpu cudatoolkit=10.1 && \
    conda clean -ya


WORKDIR /workspace
CMD ["/bin/bash"]
