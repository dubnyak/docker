FROM httpd:2.4.35-alpine
RUN apk update \
    && apk upgrade
COPY ./apache.conf /usr/local/apache2/conf/httpd.conf
COPY ./apache/www:/var/www/html
EXPOSE 80
EXPOSE 443