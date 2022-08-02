FROM php:8.1-apache

########################################################################################################################
### DEBIAN SYSTEM ###
########################################################################################################################
#Updata Packages
RUN apt-get update

#Install Packages
RUN apt-get install -y git

#Clear Packages Data
RUN apt clean



########################################################################################################################
### APACHE SERVER ###
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

#RUN rm /etc/apache2/mods-enabled/*
#COPY apache/mods-enabled/ /etc/apache2/mods-enabled/

#RUN rm /etc/apache2/sites-enabled/*
#COPY apache/sites-enabled/ /etc/apache2/sites-enabled/



########################################################################################################################
### PHP ##
########################################################################################################################
COPY php/php.ini /usr/local/etc/php/php.ini

# XDebug
RUN pecl install -o -f xdebug-3.1.5
RUN docker-php-ext-enable xdebug
ENV XDEBUG_INI_FILE=/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.mode=develop,debug" >>  ${XDEBUG_INI_FILE} \
    && echo "xdebug.cli_color=1" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.client_host=host.docker.internal" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.client_port=10080" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.coverage_enable=1" >>  ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_enable=1" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_connect_back=1" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_log=/tmp/xdebug.log" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_autostart=true" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_host=host.docker.internal" >> ${XDEBUG_INI_FILE}



########################################################################################################################
### COMPOSER ##
########################################################################################################################
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

