# Used for DEV & Local.
FROM php:7.4-fpm as php

# Install dependencies.
RUN apt-get update && apt-get install -y unzip libpq-dev libcurl4-gnutls-dev nginx libonig-dev

# Install PHP extensions.
RUN docker-php-ext-install mysqli pdo pdo_mysql bcmath curl opcache mbstring

# Copy composer executable.
COPY --from=composer:2.3.5 /usr/bin/composer /usr/bin/composer

# Set working directory to /var/www.
WORKDIR /app

USER h5

# Copy files from current folder to container current folder (set in workdir).
COPY . .


# Create laravel caching folders.
RUN mkdir -p /var/www/storage/framework /var/www/storage/framework/cache \
    /var/www/storage/framework/testing /var/www/storage/framework/sessions \
    /var/www/storage/framework/views

# Fix files ownership.
RUN chown -R h5 /var/www/storage
RUN chown -R h5 /var/www/storage/framework
RUN chown -R h5 /var/www/storage/framework/sessions

RUN mkdir -p /var/www/storage /var/www/storage/logs /var/www/storage/framework \
    /var/www/storage/framework/sessions /var/www/bootstrap

# Fix files ownership.
RUN chown -R h5 /var/www/storage
RUN chown -R h5 /var/www/storage/framework
RUN chown -R h5 /var/www/storage/framework/sessions

# Set correct permission.
RUN chmod -R 755 /var/www/storage
RUN chmod -R 755 /var/www/storage/logs
RUN chmod -R 755 /var/www/storage/framework
RUN chmod -R 755 /var/www/storage/framework/sessions
RUN chmod -R 755 /var/www/bootstrap

# Adjust user permission & group
RUN usermod --uid 1000 h5
RUN groupmod --gid 1001 h5
