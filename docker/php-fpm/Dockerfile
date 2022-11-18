FROM php:7.4-fpm-alpine3.16
# install extensions
# intl, zip, soap
RUN apk add --update --no-cache libintl icu icu-dev libxml2-dev libmcrypt-dev libzip-dev zip\
    && docker-php-ext-install intl zip soap  mysqli pdo pdo_mysql bcmath

# mysqli, pdo, pdo_mysql
RUN apk add --update --no-cache freetype-dev libjpeg-turbo-dev libpng-dev gmp gmp-dev openssl-dev \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ --with-jpeg=/usr/include/\
    #&& pecl install mongodb \
    && docker-php-ext-install gd gmp ftp
    #&& docker-php-ext-enable mongodb\
    #&& pecl clear-cache


RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer && composer --version

RUN apk --no-cache add shadow && \
    usermod -u 1000 www-data && \
    groupmod -g 1000 www-data  \
    && rm -rf /var/cache/apk/* /tmp/*
WORKDIR /var/www