FROM php:8.0-apache

ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

RUN apt-get update -qq && \
    apt-get install -qy 

COPY ./index.php /var/www/html

EXPOSE 8080
