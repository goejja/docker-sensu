FROM animemint/sensu-testing

ARG VSPHERE_SDK_PERL=VMware-vSphere-Perl-SDK-6.5.0-4566394.x86_64.tar.gz

COPY vmware-sdk/${VSPHERE_SDK_PERL} /tmp/

RUN yum -y -d1 install python perl e2fsprogs e2fsprogs-devel libuuid-devel openssl-devel perl-devel \
  glibc.i686 zlib.i686 perl-XML-LibXML libncurses.so.5 perl-Crypt-SSLeay make which \
  perl-Module-Build perl-ExtUtils-MakeMaker perl-LWP-Protocol-https perl-JSON \
  uuid-perl perl-Crypt-OpenSSL-RSA perl-Try-Tiny perl-CPAN \
  && tar -C /tmp -xzf /tmp/${VSPHERE_SDK_PERL} \
  && sed -i 's/|| direct_command("cat \/proc\/version | grep -i ubuntu") //g' /tmp/vmware-vsphere-cli-distrib/vmware-install.pl \
  && sed -i '2621,2635d' /tmp/vmware-vsphere-cli-distrib/vmware-install.pl \
  && /tmp/vmware-vsphere-cli-distrib/vmware-install.pl -d EULA_AGREED=yes \
  && yum clean all && rm -rf /var/cache/yum \
  && rm -fr /tmp/vmware-vsphere-cli-distrib && rm -fr /tmp/VMware-*

USER sensu
CMD dockerize -template /templates/config.json.tmpl:/etc/sensu/config.json \
   /opt/sensu/bin/sensu-client -c /etc/sensu/config.json -d /etc/sensu/conf.d
