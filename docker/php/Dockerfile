FROM php:7.4-fpm

# GD
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# INTL
RUN apt-get install -y \
        libicu-dev \
    && docker-php-ext-install -j$(nproc) intl

COPY ./app /var/www/html

WORKDIR /var/www/html

CMD ["php-fpm"]

EXPOSE 9000