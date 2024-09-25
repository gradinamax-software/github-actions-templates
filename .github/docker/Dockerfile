# Use the official PHP 8.2 CLI image
FROM php:8.2-cli

# Set the working directory
WORKDIR /var/www/bekker

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    && rm -rf /var/lib/apt/lists/*

# Install PHP extensions required by Laravel
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl bcmath

# Start Laravel's built-in development server
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=80"]
