FROM php:7.4.14-fpm


# basic php extension
RUN docker-php-ext-install pdo_mysql

# Xdebug 3
ARG XDEBUG_ENABLED
ARG XDEBUG_IDEKEY
RUN if [ $XDEBUG_ENABLED = true ] ; then \
    pecl install -o -f xdebug \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host = host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey = ${XDEBUG_IDEKEY}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    ; fi

# Composer require some packages
RUN apt-get update && apt-get install -y \
    vim \
    git \
    wget \
    unzip \
    && rm -rf /var/lib/apt/lists/*

# Fix user permission
ARG USER_ID
ARG GROUP_ID
RUN groupadd -f -g $GROUP_ID user \
    && useradd -u $USER_ID -g $GROUP_ID user \
    && mkdir -p /home/user \
    && chown user:user /home/user

USER user

# Install composer
COPY --from=composer:2.0.9 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/

CMD ["php-fpm"]
