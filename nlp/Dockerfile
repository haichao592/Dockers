FROM hczhu/pytorch:pytorch1.5.1cu101-cuda10.1-cudnn7-py3.7-ubuntu18.04-runtime

ARG TRANSFORMERS=2.11.0
ARG NLP=0.3.0
ARG LIGHTNING=0.8.1
ARG HYDRA=1.0.0rc1
ARG DGL=0.4.3.post2
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir --upgrade transformers==${TRANSFORMERS} \
                                         nlp==${NLP} \
                                         pytorch-lightning==${LIGHTNING} \
                                         hydra-core==${HYDRA} \
                                         tensorboard \
                                         comet-ml \
                                         plotly \
                                         networkx \
                                         dgl-cu101==${DGL} \
                                         plotly \
                                         matplotlib && \
    pip install --no-cache-dir --upgrade hydra-nevergrad-sweeper --pre


WORKDIR /workspace
CMD ["/bin/bash"]
