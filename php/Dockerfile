FROM php:8.2-fpm

RUN apt-get update && apt-get install -y \
    vim \
    postgresql-client \
    libpq-dev \
    git \
    zip \
    unzip \
    dnsutils \
    libz-dev \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && docker-php-ext-install pdo pdo_pgsql \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN nslookup raw.githubusercontent.com

WORKDIR /var/www/html

COPY . .

RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

CMD ["php-fpm"]