FROM animemint/sensu-testing

USER sensu
CMD dockerize -template /templates/config.json.tmpl:/etc/sensu/config.json \
   /opt/sensu/bin/sensu-server -c /etc/sensu/config.json -d /etc/sensu/conf.d
