FROM telegraf:1.17

COPY ./telegraf.conf /etc/telegraf/telegraf.conf

ENTRYPOINT ["/entrypoint.sh"]

CMD ["telegraf"]