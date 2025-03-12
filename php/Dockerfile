# Базовый образ с Apache и PHP 8
FROM php:8.0-apache

# Установка необходимых расширений PHP и утилит
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libzip-dev \
    unzip \
	sendmail \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install \
    pdo \
    pdo_mysql \
    mysqli \
    gd \
    zip \
    && a2enmod rewrite

# Копирование конфигурации Apache (опционально)
COPY ./apache-config.conf /etc/apache2/sites-available/000-default.conf

# Установка рабочей директории
WORKDIR /var/www/html

# Права доступа
RUN chown -R www-data:www-data /var/www/html \
    && chmod 755 /var/www/html

# Открываем порт
EXPOSE 80