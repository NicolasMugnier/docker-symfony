FROM php:8.0-fpm
# Install modules
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        zlib1g-dev \
        libicu-dev \
        libpq-dev \
        g++ \
    && docker-php-ext-install opcache \
    && pecl install xdebug mcrypt \
    && docker-php-ext-install iconv \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install pgsql \
    #&& docker-php-ext-configure intl \
    #&& docker-php-ext-install intl \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-enable mcrypt

RUN apt-get install -y zip unzip
RUN apt-get clean -y

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

RUN usermod -u 1000 www-data

WORKDIR /var/www/html

CMD ["/usr/local/sbin/php-fpm"]
COPY ./php.ini.dev /usr/local/etc/php/php.ini