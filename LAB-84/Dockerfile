FROM php:8.4.26-apache

RUN a2dismod mpm_event 2>/dev/null; a2enmod mpm_prefork 2>/dev/null; true

COPY remote_app.php        /var/www/html/remote_app.php
COPY remote_app_enum.php   /var/www/html/enum.php
COPY check.php             /var/www/html/check.php

RUN a2enmod ssl && a2ensite default-ssl \
 && openssl req -x509 -newkey rsa:2048 -nodes -days 30 \
      -keyout /etc/ssl/private/ssl-cert-snakeoil.key \
      -out    /etc/ssl/certs/ssl-cert-snakeoil.pem \
      -subj "/CN=php2shell-lab84" 2>/dev/null

RUN chmod o+w /var/www/html \
 && printf '\nMaxRequestWorkers 256\nServerLimit 256\nStartServers 16\nMinSpareServers 8\nMaxSpareServers 32\n' >> /etc/apache2/apache2.conf

EXPOSE 80 443
