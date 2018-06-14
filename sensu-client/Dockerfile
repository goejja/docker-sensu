FROM animemint/sensu-testing AS sensu-base

ARG VSPHERE_SDK_PERL=VMware-vSphere-Perl-SDK-6.5.0-4566394.x86_64.tar.gz

COPY vmware-sdk/${VSPHERE_SDK_PERL} /tmp/

RUN apt-get install -yq --no-install-recommends python perl wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /var/tmp/*
RUN pip install --upgrade pyvmomi
RUN tar -C /tmp -xzf /tmp/${VSPHERE_SDK_PERL} \
  && sed -i '2621,2635d' /tmp/vmware-vsphere-cli-distrib/vmware-install.pl
RUN /tmp/vmware-vsphere-cli-distrib/vmware-install.pl -d EULA_AGREED=yes \
  && rm -fr /tmp/vmware-vsphere-cli-distrib && rm -fr /tmp/VMware-*


FROM sensu-base

USER sensu
CMD dockerize -template /templates/config.json.tmpl:/etc/sensu/config.json \
   /opt/sensu/bin/sensu-client -c /etc/sensu/config.json -d /etc/sensu/conf.d
