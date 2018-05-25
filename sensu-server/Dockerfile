FROM: animemint/sensu:1.4.2

CMD dockerize -template /etc/sensu/template/config.json.template:/etc/sensu/config.json \
   /opt/sensu/bin/sensu-server -c /etc/sensu/config.json -d /etc/sensu/conf.d
