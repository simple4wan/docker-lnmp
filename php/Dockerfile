FROM php:7.1-fpm-alpine

EXPOSE 9000

COPY custom.php.ini /usr/local/etc/php/conf.d/docker-php-custom.ini

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk add --update-cache --no-cache \
        autoconf g++ make util-linux-dev re2c libpng-dev icu-dev libmcrypt-dev freetype-dev \
        openssl-dev pcre-dev jpeg-dev libtool imagemagick imagemagick-dev postgresql-dev tzdata linux-headers git sudo libbsd libxml2-dev \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN git clone https://git.php.net/repository/pecl/database/mysql.git \
    && cd mysql \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && cd .. \
    && rm -rf mysql \
    && pecl install redis \
    && pecl install uuid \
    && pecl install xdebug \
    && pecl install mongodb \
    && pecl install imagick \
    && pecl install swoole \
    && docker-php-ext-enable mysql redis uuid xdebug mongodb imagick swoole

RUN wget http://www.xunsearch.com/scws/down/scws-1.2.3.tar.bz2 \
    && tar xvjf scws-1.2.3.tar.bz2 \
    && cd scws-1.2.3 \
    && ./configure --prefix=/usr/local/scws \
    && make \
    && make install \
    && cd phpext \
    && phpize \
    && ./configure --with-scws=/usr/local/scws \
    && make \
    && make install \
    && cd ../../ \
    && rm -rf scws-1.2.3 scws-1.2.3.tar.bz2 \
    && docker-php-ext-enable scws \
    && echo "scws.default.charset = utf8" >> /usr/local/etc/php/conf.d/docker-php-ext-scws.ini \
    && echo "scws.default.fpath = /usr/local/scws/etc" >> /usr/local/etc/php/conf.d/docker-php-ext-scws.ini \
    && cd /usr/local/scws/etc \
    && wget http://www.xunsearch.com/scws/down/scws-dict-chs-gbk.tar.bz2 \
    && wget http://www.xunsearch.com/scws/down/scws-dict-chs-utf8.tar.bz2 \
    && tar xvjf scws-dict-chs-gbk.tar.bz2 \
    && tar xvjf scws-dict-chs-utf8.tar.bz2 \
    && rm -rf scws-dict-chs-gbk.tar.bz2 scws-dict-chs-utf8.tar.bz2

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install intl \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install soap \
    && curl -H 'user-agent: Mozilla/5.0 (MSIE 10.0; Windows NT 6.1; Trident/5.0)' -o /usr/local/bin/composer https://dl.laravel-china.org/composer.phar \
    && chmod +x /usr/local/bin/composer

USER www-data

RUN composer config -g repo.packagist composer https://packagist.laravel-china.org \
    && composer global require "fxp/composer-asset-plugin" \
    && composer global require "symfony/var-dumper"

USER root

RUN echo "auto_prepend_file = \"/home/www-data/.composer/vendor/autoload.php\"" > /usr/local/etc/php/conf.d/docker-php-composer.ini

WORKDIR /Documents