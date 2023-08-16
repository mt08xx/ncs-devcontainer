ARG NCS_REVISION=main

# https://github.com/NordicPlayground/nrf-docker
FROM  nordicplayground/nrfconnect-sdk:${NCS_REVISION}

ENV DEBIAN_FRONTEND=noninteractive

RUN <<EOT
    apt-get -y update
    apt-get install -y qemu-system build-essential git.core libffi7
    rm -rf /var/lib/apt/lists/*
EOT


