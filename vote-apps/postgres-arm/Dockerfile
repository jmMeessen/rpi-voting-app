FROM hypriot/rpi-alpine-scratch

ENV LANG en_US.utf8
ENV PGDATA /var/lib/postgresql/data

ADD https://raw.githubusercontent.com/docker-library/postgres/master/9.4/docker-entrypoint.sh /docker-entrypoint.sh

RUN apk add --update \
    bash \
    ca-certificates \
    postgresql \
    wget \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.7/gosu-armhf" \
	&& chmod +x /usr/local/bin/gosu \
	&& apk del --purge -r ca-certificates wget \
  && mkdir -p \
    /docker-entrypoint-initdb.d \
    /run/postgresql \
  && chmod a+x /docker-entrypoint.sh \
	&& rm -rf /var/cache/apk/*



ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]
