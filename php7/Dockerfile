FROM neolao/php:7.0-fpm

MAINTAINER Stepanov Nikolai <nstepanovdev@gmail.com>

ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=app --with-fpm-group=app


RUN usermod -u 1000 -d /data -s /bin/bash www-data

RUN groupadd -r node && \
    useradd -r -g node node && \
    usermod -G www-data -a node
#RUN mkdir /data && chmod -R 644 /data && find /data -type d -exec chmod 755 {} \;

#RUN apt-get update --fix-missing && apt-get install -y \
RUN apt-get update && apt-get install -y \
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
        nodejs \
        nodejs-legacy \
        npm \
    && apt-get clean \    
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Bower & Grunt
RUN npm install -g bower gulp uglify-js uglifycss && \
    echo '{ "allow_root": true }' > /root/.bowerrc 
# Install Bundler
RUN gem install bundler

#COMPOSER
RUN curl https://getcomposer.org/installer | php -- && mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

#PHPUNIT
RUN composer global require "phpunit/phpunit"
ENV PATH /root/.composer/vendor/bin:$PATH
RUN ln -s /root/.composer/vendor/bin/phpunit /usr/bin/phpunit

COPY etc/php-fpm.conf /usr/local/etc/
COPY etc/php.ini /usr/local/etc/php/
RUN chmod ugo+rX -R /usr/local/etc/php

WORKDIR /data
CMD ["php-fpm"]
