FROM neolao/php:7.0-fpm

MAINTAINER Stepanov Nikolai <nstepanovdev@gmail.com>

ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=app --with-fpm-group=app

RUN usermod -u 1000 -d /data -s /bin/bash www-data
#RUN mkdir /data && chmod -R 775 /data && find /data -type d -exec chmod 775 {} \;

RUN apt-get update && apt-get install -y \
#RUN apt-get update --fix-missing && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        msmtp \
        imagemagick \
        libssl-dev \
        libxml2-dev \
        libicu-dev \
        libxslt-dev \
        wget git vim ruby ruby-dev libcurl4-openssl-dev \
    && apt-get clean \    
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#XDEBUG
RUN pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)\n" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/xdebug.ini \

COPY etc/php-fpm.conf /usr/local/etc/
COPY etc/php.ini /usr/local/etc/php/
RUN chmod ugo+rX -R /usr/local/etc/php

WORKDIR /data
CMD ["php-fpm"]
