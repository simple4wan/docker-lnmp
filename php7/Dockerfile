FROM php:7-fpm

RUN apt update && apt install -y \
    libmagickwand-dev uuid-dev libpng-dev libzip-dev libpq-dev git

RUN pecl install imagick \
    && pecl install mongodb \
    && pecl install redis \
    && pecl install swoole-4.8.11 \
    && pecl install uuid \
    && pecl install xdebug \
    && docker-php-ext-enable imagick mongodb redis swoole uuid xdebug

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install intl \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install soap \
    && docker-php-ext-install bcmath \
    && curl -o /usr/local/bin/composer https://mirrors.aliyun.com/composer/composer.phar \
    && chmod +x /usr/local/bin/composer \
    && chown www-data:www-data -R /var/www/

USER www-data

RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && composer global require "symfony/var-dumper"

VOLUME /Documents

WORKDIR /Documents