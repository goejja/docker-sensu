FROM centos:7 AS sensu

ARG SENSU_VERSION=1.4.2-3
ARG DOCKERIZE_VERSION=0.6.1
ARG UID=1000

COPY sensu.repo /etc/yum.repos.d/
COPY templates /templates

RUN groupadd -g ${UID} sensu && useradd -r -u ${UID} -g sensu sensu \
  && yum -y -d1 update && yum -y -d1 install sensu-${SENSU_VERSION}.el7 wget \
  && yum clean all && rm -rf /var/cache/yum \
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
