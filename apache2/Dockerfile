FROM webdevops/apache:ubuntu-18.04

LABEL maintainer="Eric Pfeiffer <computerfr33k@users.noreply.github.com>"

ARG PHP_UPSTREAM_CONTAINER=php-fpm
ARG PHP_UPSTREAM_PORT=9000
ARG PHP_UPSTREAM_TIMEOUT=60
ARG DOCUMENT_ROOT=/var/www/

ENV WEB_PHP_SOCKET=${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}

ENV WEB_DOCUMENT_ROOT=${DOCUMENT_ROOT}

ENV WEB_PHP_TIMEOUT=${PHP_UPSTREAM_TIMEOUT}

EXPOSE 80 443

WORKDIR /var/www/

COPY vhost.conf /etc/apache2/sites-enabled/vhost.conf

# NawattY custom - start

# # add ssl - start
# RUN mkdir /etc/apache2/ssl 2> /dev/null
# RUN openssl genrsa -out "/etc/apache2/ssl/ssl_local.key" 2048 \
#    && openssl req -new -key "/etc/apache2/ssl/ssl_local.key" -out "/etc/apache2/ssl/ssl_local.csr" -subj "/CN=*.example.test/O=LGS/C=TH" \
#    && openssl x509 -req -days 365 -in "/etc/apache2/ssl/ssl_local.csr" -signkey "/etc/apache2/ssl/ssl_local.key" -out "/etc/apache2/ssl/ssl_local.crt"
# # add ssl - end

# # add ssl - start
# RUN apt-get update
# RUN apt install libnss3-tools -y
# RUN wget https://github.com/FiloSottile/mkcert/releases/download/v1.4.1/mkcert-v1.4.1-linux-amd64
# RUN mv mkcert-v1.4.1-linux-amd64 mkcert
# RUN chmod +x mkcert
# RUN cp mkcert /usr/local/bin/
# RUN mkdir /etc/apache2/ssl
# RUN mkcert -install
# RUN mkcert -key-file "/etc/apache2/ssl/ssl_local.key" -cert-file "/etc/apache2/ssl/ssl_local.crt" "*.example.test" example.test localhost 127.0.0.1 ::1
# # add ssl - end

# RUN a2enmod rewrite && a2enmod headers && a2enmod proxy proxy_html proxy_http xml2enc
# RUN a2enmod ssl
# RUN service apache2 restart

# NawattY custom - end

ENTRYPOINT ["/opt/docker/bin/entrypoint.sh"]

CMD ["supervisord"]
