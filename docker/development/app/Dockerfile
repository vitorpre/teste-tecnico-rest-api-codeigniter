FROM php:8.2-apache

RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd mbstring pdo pdo_mysql mysqli intl

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer
COPY docker/development/app/default.conf /etc/apache2/sites-available/000-default.conf

RUN a2enmod rewrite

COPY . /var/www/html

RUN chown -R www-data:www-data /var/www/html

WORKDIR /var/www/html

RUN composer install

EXPOSE 80

CMD ["apache2-foreground"]