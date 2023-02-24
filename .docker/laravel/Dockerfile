FROM php:8.2-fpm-alpine

# Install PHP extensions that Laravel requires
RUN docker-php-ext-install pdo_mysql bcmath opcache

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Configure PHP
COPY ./php.ini $PHP_INI_DIR/conf.d/opcache.ini

# Use the default development configuration
RUN mv $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini

# Update Alpine repository and install bash
RUN apk update && apk add --no-cache bash

# Install Node.js and npm
RUN apk add --no-cache nodejs npm

# Install pnpm
RUN npm install -g pnpm

# Create user based on provided user ID
ARG HOST_UID
RUN adduser -D -g "" -u $HOST_UID laravel

# Switch to that user
USER laravel