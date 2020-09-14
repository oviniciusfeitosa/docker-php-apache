FROM php:7.4-apache

#VOLUME ["/var/www"]

# RUN apt-get update

# RUN echo "[ ***** ***** ***** ] - Installing each item in new command to use cache and avoid download again ***** ***** ***** "
# RUN apt-get install -y apt-utils \
#   && libjpeg62-turbo-dev \
#   && libcurl4-gnutls-dev \
#   && libxml2-dev \
#   && freetds-dev \
#   && git \
#   && curl

# RUN echo "[ ***** ***** ***** ] - Installing PHP Dependencies ***** ***** ***** "
# RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
# RUN docker-php-ext-install gd \
#   && soap

# RUN docker-php-ext-install calendar
# #RUN docker-php-ext-configure mssql --with-libdir=/lib/x86_64-linux-gnu && docker-php-ext-install mssql
# RUN docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu && docker-php-ext-install pdo_dblib
# RUN docker-php-ext-install zip
RUN docker-php-ext-install mysqli

WORKDIR /tmp/
RUN ls -la /tmp
RUN curl --silent --show-error https://getcomposer.org/installer | php
RUN ls -la /tmp/composer.phar
RUN mv /tmp/composer.phar /usr/local/bin/
RUN ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

WORKDIR /var/www/

EXPOSE 80
EXPOSE 9000

#COPY . /var/www/app
RUN mkdir -p /var/www/app

RUN chmod +x -R /var/www/app

COPY ./docker/apache2/conf-available/security.conf /etc/apache2/conf-available/security.conf
COPY ./docker/apache2/sites-available/site.conf /etc/apache2/sites-available/site.conf

RUN a2ensite site.conf
RUN a2dissite 000-default.conf
RUN a2enmod rewrite
RUN a2enmod headers
# RUN cd /var/www/app && composer install --prefer-source --no-interaction

#COPY ./docker/docker-entrypoint.sh /usr/local/bin/
#ENTRYPOINT ["docker-entrypoint.sh"]

CMD apachectl -DFOREGROUND