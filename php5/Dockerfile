FROM neolao/php:5.6-fpm
MAINTAINER Stepanov Nikolai <nstepanovdev@gmail.com>

ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=app --with-fpm-group=app

RUN groupadd -g 1000 app && \
    useradd -g 1000 -u 1000 -d /data -s /bin/bash app

RUN apt-get update --fix-missing && apt-get install -y \
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
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install mcrypt mysql mysqli pdo_mysql mbstring ftp soap zip opcache intl xsl \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# Install xdebug
RUN pecl install xdebug \
    && rm -rf /tmp/pear

# Enable debug extension
RUN echo ";zend_extension=`ls /usr/local/lib/php/extensions/no-debug-non-zts-*/xdebug.so`" > /usr/local/etc/php/conf.d/xdebug.ini


COPY etc/php-fpm.conf /usr/local/etc/
COPY etc/php.ini /usr/local/etc/php/
RUN chmod ugo+rX -R /usr/local/etc/php

WORKDIR /data
CMD ["php-fpm"]

