# Use the official image as a parent image
FROM php:8.2-fpm-alpine

# Install system dependencies
RUN apt update && apt install -y git curl libjpeg-dev libfreetype6-dev zip unzip

# Clear cache
RUN apt clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd pdo pdo_mysql

# Set working directory
WORKDIR /var/wwww

# Remove default nginx website
RUN rm -rf /var/www/html

# Install Composer
RUN curl -sS https://getcomposer.org/download/ | php -- --install-dir=/usr/local/bin --filename=composer

# Install Composer from the official image
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy existing application directory contents
COPY . /var/www/

# Copy existing application directory permissions
COPY --chown=www-data:www-data . /var/www

# Install PHP dependencies
RUN composer install