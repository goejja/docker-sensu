FROM animemint/sensu:1.4.2-3

RUN apt-get install -y --no-install-recommands python-requests kmod \
  libssl-dev libxml-libxml-perl libcrypt-ssleay-perl libsoap-lite-perl \
  libdata-compare-perl libmodule-build-perl lib32z1 lib32ncurses5 libjson-perl \
  libcrypt-openssl-rsa-perl libdata-uuid-libuuid-perl liblist-moreutils-perl \
  libextutils-makemaker-cpanfile-perl  liblwp-protocol-https-perl \
  perl perl-doc uuid uuid-dev iputils-ping make \
  && rm -rf /var/lib/apt/lists/* \
  && echo ubuntu > /etc/fake-release

CMD dockerize -template /templates/config.json.tmpl:/etc/sensu/config.json \
   /opt/sensu/bin/sensu-client -c /etc/sensu/config.json -d /etc/sensu/conf.d
