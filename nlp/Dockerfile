ARG BASE
FROM ${BASE}

RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir --upgrade transformers \
                                         datasets \
                                         nltk \
                                         spacy \
                                         pytorch-lightning \
                                         hydra-core \
                                         comet-ml \
                                         optuna \
                                         jedi==0.17.2 && \
    pip install --no-cache-dir --upgrade hydra-nevergrad-sweeper hydra-joblib-launcher --pre && \
    conda install -c pytorch faiss-gpu cudatoolkit=10.1 && \
    conda install -c dglteam dgl-cuda10.1 && \
    conda clean -ya


WORKDIR /workspace
CMD ["/bin/bash"]
