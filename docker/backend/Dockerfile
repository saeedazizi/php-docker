FROM php:7.4.5-fpm

# Set working directory
WORKDIR /var/www

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install dependencies
RUN apt-get update  && apt-get install -yq --fix-missing \
    build-essential \
    libpng-dev \
    libonig-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libmcrypt-dev \
    zlib1g-dev \
    libxml2-dev \
    libzip-dev \
    libcurl4 \
    libcurl4-openssl-dev \
    locales \
    jpegoptim optipng pngquant gifsicle \
    unzip \
    vim \
    git \
    curl \
    gnupg2 \
    nodejs

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get install -yq yarn

RUN curl -L https://npmjs.org/install.sh | sh

RUN pecl install xdebug && docker-php-ext-enable xdebug

# Install extensions
RUN docker-php-ext-install pdo_mysql zip exif pcntl
RUN docker-php-ext-configure gd --with-freetype --with-jpeg 
RUN docker-php-ext-install gd
RUN docker-php-ext-install soap
RUN docker-php-ext-install curl
RUN docker-php-ext-install bcmath
# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
# RUN groupadd -g 1000 www
# RUN useradd -u 1000 -ms /bin/bash -g www www

# Copy existing application directory permissions
# COPY --chown=www:www . /var/www

# Change current user to www
# USER user

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
