FROM php:7.2.2-apache

RUN apt update

COPY ./apache.conf /usr/local/apache2/conf/httpd.conf
COPY ./www /var/www/html
EXPOSE 80
EXPOSE 443