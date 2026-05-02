# Use official Ubuntu base image
FROM docker.io/ubuntu

# Install dependencies in a single layer
RUN apt-get update && apt-get install apache2 -y

# Configure Apache to listen on port 8080 instead of 80
RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf \
    && sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8080>/g' /etc/apache2/sites-available/000-default.conf

# Copy website files into Apache root
COPY src/ /var/www/html/

# Ensure required directories exist and permissions are correct
RUN mkdir -p /var/run/apache2 /var/log/apache2 \
    && chown -R www-data:www-data /var/run/apache2 /var/log/apache2 /var/www/html \
    && chmod -R 755 /var/run/apache2 /var/log/apache2

# Expose Apache port
EXPOSE 8080

# Run as non-root user
USER www-data:www-data

# Start Apache in foreground
CMD ["apache2ctl", "-D", "FOREGROUND"]

# Optional volume for web content
VOLUME ["/var/www/html"]
