FROM centos:7 AS sensu

ARG SENSU_VERSION=1.4.2-3
ARG DOCKERIZE_VERSION=0.6.1
ARG UID=1000

COPY sensu.repo /etc/yum.repos.d/
COPY templates /templates

RUN groupadd -g ${UID} sensu && useradd -r -u ${UID} -g sensu sensu
RUN yum -y update && yum -y install sensu-${SENSU_VERSION}.el7 wget
RUN yum clean all
RUN rm -rf /var/cache/yum
RUN wget https://github.com/jwilder/dockerize/releases/download/v${DOCKERIZE_VERSION}/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz
RUN tar -C /usr/local/bin -xzf dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz
RUN rm -rf /dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz

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

FROM sensu AS sensu-server

USER sensu
CMD dockerize -template /templates/config.json.tmpl:/etc/sensu/config.json \
    /opt/sensu/bin/sensu-server -c /etc/sensu/config.json -d /etc/sensu/conf.d

FROM sensu AS sensu-api

EXPOSE 4567
USER sensu
CMD dockerize -template /templates/config.json.tmpl:/etc/sensu/config.json \
    /opt/sensu/bin/sensu-api -c /etc/sensu/config.json -d /etc/sensu/conf.d

FROM sensu AS sensu-client
USER root

ARG VSPHERE_SDK_PERL=VMware-vSphere-Perl-SDK-6.5.0-4566394.x86_64.tar.gz

COPY vmware-sdk/${VSPHERE_SDK_PERL} /tmp/

RUN yum -y install python perl e2fsprogs-devel libuuid-devel openssl-devel perl-devel \
  glibc.i686 zlib.i686 perl-XML-LibXML libncurses.so.5 perl-Crypt-SSLeay make which
RUN tar -C /tmp -xzf /tmp/${VSPHERE_SDK_PERL}
RUN sed -i '2621,2635d' /tmp/vmware-vsphere-cli-distrib/vmware-install.pl
RUN /tmp/vmware-vsphere-cli-distrib/vmware-install.pl -d EULA_AGREED=yes
RUN yum clean all
RUN rm -rf /var/cache/yum
RUN rm -fr /tmp/vmware-vsphere-cli-distrib
RUN rm -fr /tmp/VMware-*

USER sensu
CMD dockerize -template /templates/config.json.tmpl:/etc/sensu/config.json \
   /opt/sensu/bin/sensu-client -c /etc/sensu/config.json -d /etc/sensu/conf.d
