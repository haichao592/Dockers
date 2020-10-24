FROM ${BASE}

RUN apt-get update && apt-get install -y --no-install-recommends \
         openssh-server

WORKDIR /workspace
CMD ["service", "ssh", "start"]
