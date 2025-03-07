FROM php:8.2-fpm

RUN apt-get update && apt-get install -y \
    cron \
    vim \
    postgresql-client \
    libpq-dev \
    git \
    zip \
    unzip \
    dnsutils \
    libz-dev \
    libssl-dev \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && docker-php-ext-install pdo pdo_pgsql \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN nslookup raw.githubusercontent.com
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
WORKDIR /var/www/html

COPY . .

RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

RUN echo "*/5 * * * * www-data php /var/www/backend/bin/console app:flush-reactions >> /var/log/flush_reactions.log 2>&1" \
    > /etc/cron.d/flush_reactions

RUN chmod 0644 /etc/cron.d/flush_reactions && crontab /etc/cron.d/flush_reactions

CMD service cron start && php-fpm