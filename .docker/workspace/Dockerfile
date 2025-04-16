FROM php:8.2-fpm-alpine

# Set working directory
WORKDIR /var/www

# Install dependencies and PHP extensions
RUN apk update && apk add --no-cache \
    bash \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    curl \
    zip \
    git \
    icu-dev \
    libxml2-dev \
    oniguruma-dev \
    libxpm-dev \
    libzip-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo pdo_mysql mbstring zip exif pcntl gd

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Clear cache
RUN apk del icu-dev libxml2-dev oniguruma-dev && rm -rf /var/cache/apk/*

# Cấp quyền cho Laravel (chạy trong container)
RUN mkdir -p storage/logs bootstrap/cache \
    && chown -R www-data:www-data storage bootstrap/cache \
    && chmod -R 775 storage bootstrap/cache

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
