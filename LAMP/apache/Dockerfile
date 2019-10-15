FROM php:7.2.2-apache

RUN apt-get -y install libsqlite3-dev libsqlite3-0 mysql-client \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_sqlite \
    && docker-php-ext-install mysqli

COPY ./apache.conf /usr/local/apache2/conf/httpd.conf
COPY ./www /var/www/html
EXPOSE 80
EXPOSE 443