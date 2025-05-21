FROM php:8.3-fpm

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libzip-dev \
    libpq-dev \
    librabbitmq-dev \
    && docker-php-ext-install  \
    zip \
    pdo \
    pdo_pgsql \
    && rm -rf /var/lib/apt/lists/*

# Установка Redis расширения
RUN pecl install redis && docker-php-ext-enable redis

# Установка AMQP расширения
RUN pecl install amqp && docker-php-ext-enable amqp

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

RUN apt-get update && \
    apt-get install -y  && \
    docker-php-ext-install pdo pdo_mysql