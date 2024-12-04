# Use an official PHP image with Apache as the base image.
FROM php:8.2-apache

# Install system dependencies. We want MySQL CLI so we can communicate with container on socket via Docker from outside.
RUN apt-get update && \
    apt-get install -y git default-mysql-client

# Install PHP extensions.  This is key because REDCap uses MySQLi
RUN docker-php-ext-install -j$(nproc) mysqli

# Configure Mailhog
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.19.4.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go install github.com/mailhog/mhsendmail@v0.2.0
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail

# Copy a php.ini and set the Mailhog path
COPY php.ini /usr/local/etc/php
RUN echo "sendmail_path = '/usr/bin/mhsendmail --smtp-addr=mailhog:1025'" >> /usr/local/etc/php/php.ini

# Set up the entrypoint
COPY ./docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod -x /docker-entrypoint.sh

# Expose port 80 for Apache.
EXPOSE 80

# Start Apache web server.
CMD ["/docker-entrypoint.sh"]