# Use an official PHP 8.1 image as the base image
FROM php:8.1-apache

# Set the working directory inside the container
WORKDIR /var/www/html

# Copy the CodeIgniter 4 application files into the container
COPY framework_files/app_files/ .

# Install any necessary dependencies
COPY framework_files/requirements.txt /tmp/
RUN apt-get update && \
    apt-get install -y \
    # Include any necessary packages here (e.g., libraries, tools) \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install mysqli pdo pdo_mysql \
    # Install Composer (if necessary)
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    # Install dependencies using Composer (if required)
    && composer install --no-interaction --optimize-autoloader

# Set proper permissions if needed
RUN chown -R www-data:www-data /var/www/html

# Expose port 8080 to the outside world
EXPOSE 8080

# Start Apache service
CMD ["apache2-foreground"]
