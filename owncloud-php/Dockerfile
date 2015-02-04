FROM debian:testing
MAINTAINER Jonathan Dray <jonathan.dray@gmail.com>

# Configure APT
ENV DEBIAN_FRONTEND noninteractive
RUN echo 'APT::Install-Recommends "0";\nAPT::Install-Suggests "0";' | tee -a /etc/apt/apt.conf

# Base setup
# ADD resources/etc/apt/ /etc/apt/
RUN apt-get -y update && \
apt-get install -q -y locales ca-certificates bzip2 wget unzip openssl ssl-cert

# php packages for php-fpm with owncloud requirements
RUN apt-get install -q -y php5-fpm php5-gd php-xml-parser php5-intl php5-curl php5-json php5-mcrypt php5-pgsql

# Cleanup
# Remove package cache
RUN apt-get clean && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# PHP-FPM config
COPY etc/php5/fpm/php-fpm.conf /etc/php5/fpm/php-fpm.conf
COPY etc/php5/fpm/pool.d/www.conf /etc/php5/fpm/pool.d/www.conf
# RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini && \
# sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf

# Working directory
RUN mkdir -p /var/www/html && chown www-data: /var/www/html
WORKDIR /var/www/html

# Will listen on port 9000
EXPOSE 9000

# Command to start on container default run
CMD ["php5-fpm"]
