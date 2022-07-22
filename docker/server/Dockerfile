FROM httpd:2.4-bullseye



########################################################################################################################
### DEBIAN ###
########################################################################################################################
#Updata Packages
RUN apt-get update
RUN apt-get -y upgrade

#Install Packages
RUN apt-get install -y git

#Clear Packages Data
RUN apt clean



########################################################################################################################
### APACHE ###
########################################################################################################################
# Configuration Files #
#######################
# /etc/apache2/
#   apache.conf
#   envvars
#   magic
#   ports.conf
#   conf-available/
#   conf-enabled/
#   mods-available/
#   mods-enabled/
#   sites-available/
#   Sites-enabled/
#######################
# Log Files #
#######################
# /var/log/apache2/
#   access.log
#   error.log
########################################################################################################################
#RUN rm /etc/apache2/conf-enabled/*
#COPY apache/conf-enabled/ /etc/apache2/conf-enabled/
#
#RUN rm /etc/apache2/mods-enabled/*
#COPY apache/mods-enabled/ /etc/apache2/mods-enabled/
#
#RUN rm /etc/apache2/sites-enabled/*
#COPY apache/sites-enabled/ /etc/apache2/sites-enabled/



########################################################################################################################
### PHP ##
########################################################################################################################
RUN apt-get install -y libapache2-mod-php
RUN a2enmod php7.*
#RUN systemctl restart apache2
#COPY php/php.ini /usr/local/etc/php/php.ini

# XDEBUG
#RUN pecl install -o -f xdebug
#RUN docker-php-ext-enable xdebug
#ENV XDEBUG_INI_FILE=/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.remote_port=10080" >> ${XDEBUG_INI_FILE} \
#    && echo "xdebug.mode=coverage" >>  ${XDEBUG_INI_FILE} \
#    && echo "xdebug.coverage_enable=1" >>  ${XDEBUG_INI_FILE} \
#    && echo "xdebug.remote_enable=1" >> ${XDEBUG_INI_FILE} \
#    && echo "xdebug.remote_connect_back=1" >> ${XDEBUG_INI_FILE} \
#    && echo "xdebug.remote_log=/tmp/xdebug.log" >> ${XDEBUG_INI_FILE} \
#    && echo "xdebug.remote_autostart=true" >> ${XDEBUG_INI_FILE} \
#    && echo "xdebug.remote_host=host.docker.internal" >> ${XDEBUG_INI_FILE}



########################################################################################################################
### COMPOSER ##
########################################################################################################################
#COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

