FROM php:8.2-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libzip-dev \
    && docker-php-ext-install zip pdo pdo_mysql

WORKDIR /var/www/html

# Copy backend source
COPY . .

# Install Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Install PHP dependencies (ignore platform reqs for learning)
RUN composer install --no-interaction --no-scripts || true

EXPOSE 9000

CMD ["php-fpm"]
