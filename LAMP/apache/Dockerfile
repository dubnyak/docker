FROM php:7.2.2-apache

RUN apt update
RUN apt-get -y install libsqlite3-dev libsqlite3-0 mysql-client \
    && docker-php-ext-install -j$(nproc) iconv intl xml soap mcrypt opcache pdo pdo_mysql mysqli mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

COPY ./apache.conf /usr/local/apache2/conf/httpd.conf
COPY ./www /var/www/html
EXPOSE 80
EXPOSE 443