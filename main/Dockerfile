FROM ubuntu:18.04
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y ubuntu-server nano curl git zip unzip gnupg
RUN apt-get upgrade -y

# PHP
RUN add-apt-repository ppa:ondrej/php
RUN apt-get install -y php7.3 php7.3-mbstring php7.3-xml php7.3-mysql

# Apache2
RUN apt-get install -y apache2

# Install app -clear app directory
RUN rm -rf /var/www/*

#set vhost
RUN rm /etc/apache2/sites-available/000-default.conf
COPY ./httpd-project.conf /etc/apache2/sites-available/httpd-project.conf
RUN ln -sf /etc/apache2/sites-available/httpd-project.conf /etc/apache2/sites-enabled/httpd-project.conf
RUN a2enmod rewrite

# Configure apache
RUN chown -R www-data:www-data /var/www
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
CMD apachectl -D FOREGROUND

# mysql-client
RUN apt-get install -y mariadb-client
# logowanie: mysql - u USER - h HOST DATABASE_NAME -p PASSWORD

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# NPM
RUN curl -sL https://deb.nodesource.com/setup_12.x  | bash -
RUN apt-get -y install nodejs

WORKDIR /var/www/
