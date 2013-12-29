FROM tianon/debian:jessie

MAINTAINER Jonathan Dray <jonathan.dray@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
RUN sed -i 's/ftp.us/ftp.fr/g' /etc/apt/sources.list
RUN apt-get -y update

# System locales configuration
RUN apt-get install -y --no-install-recommends locales


# Install packages requirements
RUN apt-get install -y --no-install-recommends bzip2 wget vim openssl ssl-cert sharutils curl


# NGINX install
RUN apt-get install -y --no-install-recommends nginx

RUN mkdir /etc/nginx/ssl
ADD resources/ssl/ /etc/nginx/ssl/
ADD resources/etc/nginx/sites-available/ /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/001-owncloud /etc/nginx/sites-enabled/

# nginx config
RUN sed -i -e"s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf
# since 'upload_max_filesize = 2M' in /etc/php5/fpm/php.ini
RUN sed -i -e"s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 3m/" /etc/nginx/nginx.conf
# disable daemon mode
RUN echo "daemon off;" >> /etc/nginx/nginx.conf


# PHP packages
RUN apt-get install -y --no-install-recommends php5-fpm php5-gd php-xml-parser php5-intl php5-curl php5-json php5-mcrypt

# php-fpm config
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf


# Postgresql install
RUN apt-get install -y --no-install-recommends postgresql php5-pgsql

# Initialize postgres database for owncloud
ADD resources/sql/owncloud-postgresql.sql /tmp/
RUN /etc/init.d/postgresql start && sleep 2 && su postgres -c "cd /tmp ; psql -a -f owncloud-postgresql.sql &&  exit"

# Hack posgresql configuration so it can be launched in foreground mode
RUN sed -i 's/^auto.*$/manual/g' /etc/postgresql/9.3/main/start.conf

# Add shell script to launch postgres in foreground mode
ADD resources/usr/local/bin/postgresql.sh /usr/local/bin/
RUN chmod 0755 /usr/local/bin/postgresql.sh


# Get latest owncloud release
RUN mkdir /var/www /data
# Create a volume to share with other containers
VOLUME ["/data"]

RUN wget -q -O - http://download.owncloud.org/community/owncloud-6.0.0a.tar.bz2 | tar jx -C /var/www
ADD resources/var/www/owncloud/config/autoconfig.php /var/www/owncloud/config/
RUN chown -R www-data: /var/www/owncloud /data


# Install supervisord
# Usefull to start and monitor multiple processes (easier than systemd in a docker context)
RUN apt-get install -y --no-install-recommends supervisor
ADD resources/etc/supervisor/ /etc/supervisor/


# Command to start on container default run
CMD ["/usr/bin/supervisord"]
