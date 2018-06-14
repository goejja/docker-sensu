FROM debian:stretch-slim AS sensu

ARG SENSU_VERSION=1.4.2-3
ARG DOCKERIZE_VERSION=0.6.1
ARG UID=1000

COPY templates /templates

RUN groupadd -g ${UID} sensu && useradd -r -u ${UID} -g sensu sensu \
  && apt-get -q update && apt-get install -yq --no-install-recommends wget ca-certificates gnupg curl \
  && curl -s https://sensu.global.ssl.fastly.net/apt/pubkey.gpg | apt-key add - \
  && echo "deb https://sensu.global.ssl.fastly.net/apt stretch main" > /etc/apt/sources.list.d/sensu.list \
  && apt-get install -yq  sensu=${SENSU_VERSION} \
  && apt-get clean && apt-get -y autoremove && rm -rf /var/lib/apt/lists/* /var/tmp/* \
  && wget https://github.com/jwilder/dockerize/releases/download/v${DOCKERIZE_VERSION}/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
  && tar -C /usr/local/bin -xzf dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
  && rm -rf /dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz

ENV RABBITMQ_HOST=rabbitmq \
    RABBITMQ_PORT=5672 \
    RABBITMQ_USER=guest \
    RABBITMQ_PASSWORD=guest \
    RABBITMQ_VHOST=/ \
    REDIS_HOST=redis \
    REDIS_PORT=6379 \
    API_HOST=sensu-api \
    API_PORT=4567 \
    TRANSPORT_NAME=rabbitmq

RUN chown -R sensu:sensu /etc/sensu
