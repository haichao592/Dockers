ARG BASE=hczhu/nlp:transformers3.1.0-datasets1.0.2-pl0.9.0-hydra1.0.2
FROM ${BASE}

RUN apt-get update && apt-get install -y --no-install-recommends build-essential cmake libxml-parser-perl

RUN yes | cpan install XML::DOM

RUN git clone https://github.com/haichao592/pyrouge && \
    cd pyrouge && \
    python setup.py install && \
    mkdir -p /opt/.pyrouge && \
    cp -r RELEASE-1.5.5 /opt/.pyrouge/ && \
    pyrouge_set_rouge_path /opt/.pyrouge/RELEASE-1.5.5 && \
    rm -rf ../pyrouge
    
ENV ROUGE_EVAL_HOME /opt/.pyrouge/RELEASE-1.5.5/data

WORKDIR /workspace
CMD ["/bin/bash"]
