FROM grafana/grafana:7.3.5

RUN wget -nv https://grafana.com/api/plugins/grafana-piechart-panel/versions/1.6.1/download -O /tmp/grafana-piechart-panel.zip
RUN unzip -q /tmp/grafana-piechart-panel.zip -d /var/lib/grafana/plugins

ENTRYPOINT ["/run.sh"]