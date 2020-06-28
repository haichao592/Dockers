FROM hczhu/nlp:nlp0.3.0-transformers2.11.0-pl0.8.1-hydra1.0.0rc1-dgl0.4.3.post2

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
