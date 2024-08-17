FROM php:8.1-apache

# Install required packages and PHP extensions
RUN apt-get update && apt-get install -y \
  libicu-dev \
  libzip-dev \
  zip \
  unzip \
  && docker-php-ext-install intl pdo pdo_mysql zip \
  && pecl install apcu \
  && docker-php-ext-enable apcu

# Enable Apache modules
RUN a2enmod rewrite ssl

# Copy SSL certificates (assuming you have them in the ssl directory)
COPY ./ssl/server.crt /etc/ssl/certs/
COPY ./ssl/server.key /etc/ssl/private/

# Configure Apache for SSL
RUN sed -i 's!/etc/ssl/certs/ssl-cert-snakeoil.pem!/etc/ssl/certs/server.crt!g' /etc/apache2/sites-available/default-ssl.conf \
  && sed -i 's!/etc/ssl/private/ssl-cert-snakeoil.key!/etc/ssl/private/server.key!g' /etc/apache2/sites-available/default-ssl.conf \
  && a2ensite default-ssl.conf

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html