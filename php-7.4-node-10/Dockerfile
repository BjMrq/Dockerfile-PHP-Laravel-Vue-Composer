FROM bjmrq/laravel:php-7.4

# Install dependencies for some Node packages
RUN apt-get update && \
  apt-get install --no-install-recommends -y \
  python-dev && \
  rm -rf /var/lib/apt/lists/*

# Get Nodejs 10 and Yarn  
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
  && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Install Nodejs and Yarn  
RUN apt-get update && \
  apt-get install -y --no-install-recommends  \
  nodejs \
  yarn  && \
  rm -rf /var/lib/apt/lists/*

# Clear cache after install
RUN apt-get autoremove -y && apt-get clean

# Expose port 9000
EXPOSE 9000

# Start php-fpm server
CMD ["php-fpm"]
