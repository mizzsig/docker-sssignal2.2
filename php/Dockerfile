FROM php:7.2.13-fpm-alpine3.8

# set Japanese time
RUN apk --update add tzdata
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN apk del tzdata
RUN rm -rf /var/cache/apk/*

# install php_mongodb extension
RUN apk add autoconf gcc g++ make
RUN pecl install mongodb
RUN docker-php-ext-enable mongodb

# install php_memcached extension
RUN apk add git zlib-dev libmemcached-dev
RUN git clone -b php7 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached
RUN docker-php-ext-configure /usr/src/php/ext/memcached --disable-memcached-sasl && \
    docker-php-ext-install /usr/src/php/ext/memcached
RUN rm -rf /usr/src/php/ext/memcached

# clone laravel project
RUN mkdir /home/mizzsig && \
    mkdir /home/mizzsig/sssignal2-2 && \
    adduser -S mizzsig

# install supervisor
RUN apk add supervisor && \
    mkdir /etc/supervisor.d && \
    mkdir /var/log/supervisor
COPY supervisor.d /etc/supervisor.d
COPY supervisord.conf /etc/supervisord.conf
