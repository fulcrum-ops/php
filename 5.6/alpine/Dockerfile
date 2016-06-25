FROM fulcrum/alpine3.4
MAINTAINER Kenn Herman "kenn@ifsight.com"

RUN echo "Cache bust 201606232004" && \
    echo '@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
    apk update && apk upgrade && \
    apk add php5 php5-fpm php5-gd php5-gettext php5-mcrypt php5-mysql php5-opcache php5-redis@testing php5-xml php5-zip postfix && \
    adduser -h /var/www/html -s /sbin/nologin -D -H -u 1971 php

ENTRYPOINT ["/usr/bin/php-fpm"]

CMD ["--nodaemonize"]
