FROM php:8.1.0-fpm

RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip vim \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu xdebug \
    && docker-php-ext-enable apcu xdebug \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

COPY php.ini /etc/php/8.1.0/php.ini
COPY xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
COPY php-fpm-pool.conf /etc/php/8.1.0/pool.d/www.conf
COPY --from=composer/composer /usr/bin/composer /usr/bin/composer

RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash && apt install symfony-cli

RUN groupadd dev -g 999
RUN useradd dev -g dev -d /home/dev -m

WORKDIR /home/www