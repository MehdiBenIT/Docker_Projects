FROM nextcloud:apache

ENV NEXTCLOUD_UPDATE=1
CMD ["/usr/bin/supervisord"]

RUN apt update
RUN "cd /var/www/nextcloud/"
RUN "sudo -u www-data php occ  maintenance:install \
--database='mysql' --database-name='nextcloud' \
--database-user='root' --database-pass='qwerty123' \
--admin-user='admin' --admin-pass='qwerty123'"
