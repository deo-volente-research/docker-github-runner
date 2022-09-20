FROM getsentry/sentry-cli:latest as sentry-cli

FROM setupphp/node:focal

COPY --from=sentry-cli /bin/sentry-cli /bin

RUN set -ex \
    && apt-get update && apt-get install -y git openssh-client dpkg-dev zip python3 python3-pip --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && pip3 install awscli

RUN apt-get update \
    && cp -r /etc/apt/sources.list.d /etc/apt/sources.list.d.save \
    && for v in 8.0 8.1; do \
           apt-get install -y --no-install-recommends php"$v" \
           php"$v"-bcmath \
           php"$v"-mbstring \
           php"$v"-pdo-mysql \
           php"$v"-gd \
           php"$v"-redis \
           php"$v"-soap \
           php"$v"-dom \
           php"$v"-cli; \
         done \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false