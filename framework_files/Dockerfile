# Use an official PHP 8.1 image as the base image with Apache
FROM php:8.1-apache

# Install the PHP intl extension
RUN apt-get update && \
    apt-get install -y libicu-dev && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl

# Set the working directory inside the container
WORKDIR /var/www/html

# Copy the CodeIgniter 4 application files into the container
COPY app_files/ .

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Run Composer to install dependencies
RUN composer install --no-scripts --no-autoloader

# Clear cache and configuration (if applicable in your CodeIgniter project)
# Replace these commands with the appropriate CodeIgniter 4 commands if needed
RUN php spark cache:clear
RUN php spark config:clear

# Generate the application key (if required in your CodeIgniter project)
RUN php spark key:generate

# Set proper permissions if needed
RUN chown -R www-data:www-data /var/www/html

# Expose port 8080 inside the container
EXPOSE 8080

# Run PHP's built-in server using `php spark serve`
CMD ["php", "spark", "serve", "--host=0.0.0.0", "--port=8080"]
