FROM busybox:latest

MAINTAINER Jonathan Dray <jonathan.dray@gmail.com>, Brendan Tobolaski <brendan@tobolaski.com>
ENV OWNCLOUD_VERSION 7.0.2
ENV ARCHIVE_CHECKSUM d0b0012972db6a1415251d3d6c49432b4f7cc3ec

RUN wget http://download.owncloud.org/community/owncloud-${OWNCLOUD_VERSION}.tar.bz2 -P /
RUN if [ `sha1sum /owncloud-${OWNCLOUD_VERSION}.tar.bz2 | awk '{print $1}'` != ${ARCHIVE_CHECKSUM} ]; \
then \
echo "checksum verification failed." && exit 1; \
else \
bzcat /owncloud-*.tar.bz2 | tar x -C /var/www -f - ; \
fi
ADD resources/var/www/owncloud/config/autoconfig.php /var/www/owncloud/config/autoconfig.php
RUN mkdir /data && \
    mv /var/www/owncloud /var/www/html && \
    chown -R www-data:www-data /var/www/html /data && \
    rm /owncloud-*.tar.bz2

VOLUME ["/var/www/html", "/data"]
