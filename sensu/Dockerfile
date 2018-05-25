FROM debian:stretch-slim

ENV SENSU_VERSION=1.4.2

RUN groupadd -r sensu && useradd -r -g sensu sensu \
  && apt-get update && apt-get install -y wget ca-certificates gnupg --no-install-recommends && rm -rf /var/lib/apt/lists/* \
  && wget -q http://sensu.global.ssl.fastly.net/apt/pubkey.gpg && apt-key add pubkey.gpg \
  && echo "deb     http://sensu.global.ssl.fastly.net/apt stretch main" > /etc/apt/sources.list.d/sensu.list \
  && apt-get update && apt-get install -y --no-install-recommends sensu=$SENSU_VERSION \
  && rm -rf /var/lib/apt/lists/*

RUN chown -R sensu:sensu /etc/sensu

