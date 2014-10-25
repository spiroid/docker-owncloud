FROM debian:testing

MAINTAINER Jonathan Dray <jonathan.dray@gmail.com>

# Configure APT
ENV DEBIAN_FRONTEND noninteractive
RUN echo 'APT::Install-Recommends "0";\nAPT::Install-Suggests "0";' | tee -a /etc/apt/apt.conf

# Base setup
# ADD resources/etc/apt/ /etc/apt/
RUN apt-get -y update && \
    apt-get install -q -y locales bzip2 wget unzip openssl ssl-cert curl

# NGINX install with php packages and supervisord to monitor php-fpm and nginx
RUN apt-get install -q -y nginx php5-fpm php5-gd php-xml-parser php5-intl php5-curl php5-json php5-mcrypt php5-pgsql supervisor

# Cleanup
# Remove package cache
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# NGINX config
# since 'upload_max_filesize = 2M' in /etc/php5/fpm/php.ini
# disable daemon mode
ADD resources/etc/nginx/sites-available/ /etc/nginx/sites-available/
RUN sed -i -e"s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf && \
    sed -i -e"s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 3m/" /etc/nginx/nginx.conf && \
    echo "daemon off;" >> /etc/nginx/nginx.conf

# PHP-FPM config
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini && \
    sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf

# Usefull to start and monitor multiple processes (easier than systemd in a docker context)
ADD resources/etc/supervisor/ /etc/supervisor/

# Command to start on container default run
CMD ["/usr/bin/supervisord"]
