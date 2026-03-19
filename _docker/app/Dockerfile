FROM php:8.2-fpm

# ---------- System deps ----------
RUN apt-get update && apt-get install -y \
    git \
    curl \
    unzip \
    libpng-dev \
    libzip-dev \
    libonig-dev \
    libpq-dev \
    libicu-dev \
    libxml2-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install \
        pdo_mysql \
        bcmath \
        gd \
        zip \
        intl \
        opcache \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# ---------- PHP config ----------
COPY ./_docker/app/php.ini /usr/local/etc/php/conf.d/php.ini

# ---------- Composer ----------
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php \
    -- --install-dir=/usr/local/bin --filename=composer

# ---------- Workdir ----------
WORKDIR /var/www

# ---------- Permissions (РІР°Р¶РЅРѕ РґР»СЏ Laravel) ----------
RUN chown -R www-data:www-data /var/www

# ---------- Expose php-fpm ----------
EXPOSE 9000

CMD ["php-fpm"]
