FROM fulcrum/centos7
MAINTAINER Kenn Herman "kenn@ifsight.com"

# Enable EPEL Repos, update, install PHP 5.6, postdrop correct perms, add the user
RUN echo "Cache bust 201605270954" && \
    yum --noplugins install -y \
        http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-7.noarch.rpm \
        http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \
    yum --noplugins --enablerepo=remi,remi-php56 -y install php php-fpm php-gd php-mbstring php-mysql php-opcache php-xml php-mcrypt php-pecl-redis php-php-gettext postfix && \
    yum --noplugins upgrade -y && \
    package-cleanup --dupes && \
    package-cleanup --cleandupes && \
    yum clean all && \
    sed -i '/^listen = /clisten = 0.0.0.0:9000' /etc/php-fpm.d/www.conf && \
    sed -i '/^listen.allowed_clients/c;listen.allowed_clients =' /etc/php-fpm.d/www.conf && \
    sed -i '/^;catch_workers_output/ccatch_workers_output = yes' /etc/php-fpm.d/www.conf && \
    chmod g+s /usr/sbin/postqueue /usr/sbin/postdrop && \
    groupadd -g 1971 php && useradd -d /var/www/html -g php -M -n -s /sbin/nologin -u 1971 php

ENTRYPOINT ["/usr/sbin/php-fpm"]
CMD ["--nodaemonize"]
