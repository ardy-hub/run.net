FROM php:8.2-cli

RUN apt-get update && apt-get install -y git curl libpng-dev libonig-dev libxml2-dev libzip-dev zip unzip && docker-php-ext-install zip pdo pdo_mysql mbstring exif pcntl bcmath

RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && apt-get install -y nodejs

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/html

COPY . .

RUN composer install --no-dev --optimize-autoloader --no-interaction

RUN if [ -f package.json ]; then npm install && npm run build; fi

RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache 2>/dev/null || true

EXPOSE 8000

CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]
