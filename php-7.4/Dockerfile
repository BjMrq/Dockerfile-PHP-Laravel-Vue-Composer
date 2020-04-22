FROM php:7.4-fpm

# Set working directory
WORKDIR /var/www

# Install dependencies for laravel
RUN apt-get update && \
  apt-get install --no-install-recommends -y \
  apt-utils \
  build-essential \
  default-mysql-client \
  mariadb-client \
  libonig-dev \
  libpng-dev \
  libzip-dev \
  libjpeg62-turbo-dev \
  libfreetype6-dev \
  locales \
  zip \
  jpegoptim optipng pngquant gifsicle \
  vim \
  unzip \
  git \
  curl \
  graphviz \
  openssh-client && \
  rm -rf /var/lib/apt/lists/*

# Clear cache
# Clean after install
RUN apt-get autoremove -y && apt-get clean

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php && \
  mv composer.phar /usr/local/bin/composer
# Install Prestissimo globally for faster Composer install
RUN composer global require hirak/prestissimo --no-plugins --no-scripts

# Expose port 9000
EXPOSE 9000

# Start php-fpm server
CMD ["php-fpm"]
