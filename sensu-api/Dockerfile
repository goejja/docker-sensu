FROM animemint/sensu-testing

EXPOSE 4567

USER sensu
CMD dockerize -template /templates/config.json.tmpl:/etc/sensu/config.json \
    /opt/sensu/bin/sensu-api -c /etc/sensu/config.json -d /etc/sensu/conf.d
