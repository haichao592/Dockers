ARG BASE
FROM ${BASE}

RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir --upgrade transformers==4.5.0 \
                                         datasets \
                                         nltk \
                                         spacy \
                                         pytorch-lightning==1.2.8 \
                                         comet-ml \
                                         dgl-cu111 \
                                         optuna && \
    conda install -c conda-forge faiss-gpu cudatoolkit=11.1 && \
    conda clean -ya


WORKDIR /workspace
CMD ["/bin/bash"]
