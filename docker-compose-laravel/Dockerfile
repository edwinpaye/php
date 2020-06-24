FROM php:7.4-fpm-alpine
# COPY ./src/ /var/www/html
RUN chown -R www-data:www-data /var/www/html

WORKDIR /var/www/html

RUN docker-php-ext-install pdo pdo_mysql
