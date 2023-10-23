FROM node:14-alpine AS node
FROM composer:2.3 AS composer

FROM php:8.2-fpm-alpine

COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY --from=node /usr/lib           /usr/lib
COPY --from=node /usr/local/share   /usr/local/share
COPY --from=node /usr/local/lib     /usr/local/lib
COPY --from=node /usr/local/include /usr/local/include
COPY --from=node /usr/local/bin     /usr/local/bin

RUN apk update --no-cache && apk add --no-cache \
    curl \
    supervisor \
    unzip \
#    python \
    g++ \
    make \
    nginx \
    yarn \
    php \
#    php-apcu \
    php82-calendar \
    php82-common \
    php82-cli \
    php82-common \
    php82-ctype \
    php82-curl \
    php82-dom \
    php82-exif \
    php82-fileinfo \
    php82-fpm \
    php82-gd \
    php82-intl \
    php82-mbstring \
    php82-mysqli \
    php82-mysqlnd \
    php82-opcache \
    php82-pdo \
    php82-pdo_mysql \
    php82-pdo_pgsql \
    php82-pgsql \
    php82-phar \
    php82-session \
    php82-simplexml \
    php82-sqlite3 \
    php82-tokenizer \
    php82-xml \
    php82-xmlwriter \
    php82-xsl \
    php82-zip

RUN rm -rf /var/lib/apk/lists/* /tmp/* /var/tmp/* /usr/share/doc/* /usr/share/man/* /var/cache/apk/*

RUN ln -s /usr/local/sbin/php-fpm /usr/sbin/php-fpm \
#    && ln -s /usr/bin/php8 /usr/bin/php \
    && mkdir -p /run/php /var/log/php-fpm

#RUN adduser -u 1000 -D -S -G www-data www-data

COPY .docker/supervisord.conf   /etc/supervisor/conf.d/supervisor.conf
COPY .docker/nginx.conf         /etc/nginx/nginx.conf
COPY .docker/php-fpm.conf       /etc/php8/php-fpm.conf
COPY .docker/php.ini            /etc/php8/php.ini

WORKDIR /app

EXPOSE 80

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisor.conf"]
