FROM php:7.3-fpm

# Set working directory
WORKDIR /var/www

# Install dependencies for laravel
RUN apt-get update && \
  apt-get install --no-install-recommends -y \
  apt-utils \
  build-essential \
  default-mysql-client \
  mariadb-client \
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

# Clear cache after install
RUN apt-get autoremove -y && apt-get clean 

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
RUN docker-php-ext-install gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# Install Prestissimo globally for faster Composer install
RUN composer global require hirak/prestissimo

# Install Xdebug
RUN pecl install xdebug \
  && docker-php-ext-enable xdebug

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]