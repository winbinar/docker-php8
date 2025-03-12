FROM php:8.2-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd mysqli

# Copy PHP configuration
COPY php.ini /usr/local/etc/php/

# Copy application code
COPY . /var/www/html