ARG BASE=hczhu/nlp:latest
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
