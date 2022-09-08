FROM setupphp/node:focal

RUN set -ex \
    && apt-get update && apt-get install -y git openssh-client dpkg-dev zip python3 python3-pip --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && pip3 install awscli