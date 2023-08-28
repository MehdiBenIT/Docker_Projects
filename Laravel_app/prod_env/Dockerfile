# Use the official PHP image from the dockerhub
FROM php:8.2-fpm-alpine

# Install system dependencies and PHP extensions
RUN apk --no-cache add git libzip-dev zip \
    && docker-php-ext-install pdo pdo_mysql

# Set working directory
WORKDIR /var/www

# Install Composer globally
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy composer.json and composer.lock files to the container
COPY composer.json composer.lock ./

# Install project dependencies
RUN composer install --no-ansi --no-interaction --no-scripts --no-suggest --no-dev --optimize-autoloader

# Copy local code to the container
COPY . .

# Change owner and permissions for storage and bootstrap cache
RUN chown -R www-data:www-data /var/www/storage \
    && chown -R www-data:www-data /var/www/bootstrap/cache

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]