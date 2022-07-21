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
RUN rm /etc/apache2/conf-enabled/*
COPY apache/conf-enabled/ /etc/apache2/conf-enabled/

RUN rm /etc/apache2/mods-enabled/*
COPY apache/mods-enabled/ /etc/apache2/mods-enabled/

RUN rm /etc/apache2/sites-enabled/*
COPY apache/sites-enabled/ /etc/apache2/sites-enabled/



########################################################################################################################
### PHP ##
########################################################################################################################
#...



########################################################################################################################
### COMPOSER ##
########################################################################################################################
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

