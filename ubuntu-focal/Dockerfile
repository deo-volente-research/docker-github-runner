FROM setupphp/node:focal

RUN set -ex \
    && apt-get update && apt-get install -y git dpkg-dev zip python3 python3-pip openssh-client --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && pip3 install awscli \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false