# Use the official PHP 8.2 FPM image
FROM php:8.2-fpm

# Set the working directory
WORKDIR /var/www/bekker

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    curl \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    nginx \
    && rm -rf /var/lib/apt/lists/*

# Install PHP extensions required by Laravel
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl bcmath

# Install Redis extension with igbinary support via PECL
RUN pecl install redis && pecl install igbinary && docker-php-ext-enable redis igbinary

# Install nvm, Node.js, and Yarn
ENV NVM_DIR /root/.nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install --lts \
    && nvm use --lts \
    && npm install -g yarn

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy project files
COPY . .

# Copy Nginx configuration file
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx and PHP-FPM
CMD ["bash", "-c", "service nginx start && php-fpm"]
