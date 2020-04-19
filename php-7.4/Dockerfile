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
  openssh-client \
  --no-install-recommends && \
  rm -rf /var/lib/apt/lists/*

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
  && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update \
  && apt-get install -y --no-install-recommends  \
  nodejs \
  yarn  && \
  rm -rf /var/lib/apt/lists/*

# Clear cache
# Clean after install
RUN apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Tiny allows to gracefully stop node process
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

# Tiny entrypoint
ENTRYPOINT ["/tini", "--"]

# Install Xdebug
RUN pecl install xdebug \
  && docker-php-ext-enable xdebug

# Expose port 9000
EXPOSE 9000

# Start php-fpm server
CMD ["php-fpm"]
