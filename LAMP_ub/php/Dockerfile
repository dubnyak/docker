FROM php:7.3-rc-fpm-alpine
RUN apk update \
    && apk upgrade \
    && docker-php-ext-install mysqli \
    && apk add freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
COPY php.ini /usr/local/etc/php/php.ini 