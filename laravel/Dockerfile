
FROM php:8.2-cli

#  php extensions
RUN apt-get update && apt-get install -y \
    unzip git curl libicu-dev libzip-dev libpng-dev libjpeg-dev libfreetype6-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo pdo_mysql bcmath intl zip gd \
    && rm -rf /var/lib/apt/lists/*

# composer
COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer

WORKDIR /app
COPY . .

# instasll dependencies
RUN composer install

# permissions
RUN chmod -R 775 storage bootstrap/cache
EXPOSE 8000

CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]