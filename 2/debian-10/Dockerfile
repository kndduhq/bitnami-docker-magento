FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages acl ca-certificates cron curl gzip libaudit1 libbsd0 libbz2-1.0 libc6 libcap-ng0 libcom-err2 libcurl4 libexpat1 libffi6 libfftw3-double3 libfontconfig1 libfreetype6 libgcc1 libgcrypt20 libglib2.0-0 libgmp10 libgnutls30 libgomp1 libgpg-error0 libgssapi-krb5-2 libhogweed4 libicu63 libidn2-0 libjemalloc2 libjpeg62-turbo libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 liblcms2-2 libldap-2.4-2 liblqr-1-0 libltdl7 liblzma5 libmagickcore-6.q16-6 libmagickwand-6.q16-6 libmcrypt4 libmemcached11 libmemcachedutil2 libncurses6 libnettle6 libnghttp2-14 libonig5 libp11-kit0 libpam0g libpcre3 libpng16-16 libpq5 libpsl5 libreadline7 librtmp1 libsasl2-2 libsodium23 libsqlite3-0 libssh2-1 libssl1.1 libstdc++6 libsybdb5 libtasn1-6 libtidy5deb1 libtinfo6 libunistring2 libuuid1 libwebp6 libx11-6 libxau6 libxcb1 libxdmcp6 libxext6 libxml2 libxslt1.1 libzip4 procps tar zlib1g
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "php" "7.4.26-3" --checksum c8d79adeecf3f36ff8df387c105398c9f45eb344990f5d1980d3919d556387ae
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "apache" "2.4.51-7" --checksum 1b827e70d1633dc9c3035458ccf893dbb0d503b5dbfa01109eecb356e1e1a0db
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "wait-for-port" "1.0.1-3" --checksum 9e18c6c3411e702eb16aa60dc77baf3fd9af8d5beb2623936ef3af343d5ffd5b
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "mysql-client" "10.3.32-0" --checksum 4a211faa9436c9747dfc4374cb9e8a7f9b0065dfc58dd4784cef0f5029c2e65e
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "libphp" "7.4.26-0" --checksum e30f91e2e21a90772e04b795c2db35d1f0f5d934f4fcb2a1d872e50c32fc8bff
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "render-template" "1.0.1-3" --checksum cddf51b3cb59d65d5d30e3fe37e99d8d53375ad88f0cc474019a52e6d8b4fc58
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "magento" "2.4.3-2" --checksum 037b1d1dc8e3a37b384e4990a38eca829b920dc0de7e103bfef894c4eda3fd1d
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.14.0-0" --checksum 3e6fc37ca073b10a73a804d39c2f0c028947a1a596382a4f8ebe43dfbaa3a25e
RUN chmod g+rwX /opt/bitnami
RUN sed -i -e '/pam_loginuid.so/ s/^#*/#/' /etc/pam.d/cron

COPY rootfs /
RUN /opt/bitnami/scripts/php/postunpack.sh
RUN /opt/bitnami/scripts/apache/postunpack.sh
RUN /opt/bitnami/scripts/apache-modphp/postunpack.sh
RUN /opt/bitnami/scripts/magento/postunpack.sh
RUN /opt/bitnami/scripts/mysql-client/postunpack.sh
ENV ALLOW_EMPTY_PASSWORD="no" \
    APACHE_ENABLE_CUSTOM_PORTS="no" \
    APACHE_HTTPS_PORT_NUMBER="" \
    APACHE_HTTP_PORT_NUMBER="" \
    BITNAMI_APP_NAME="magento" \
    BITNAMI_IMAGE_VERSION="2.4.3-debian-10-r66" \
    MARIADB_HOST="mariadb" \
    MARIADB_PORT_NUMBER="3306" \
    MARIADB_ROOT_PASSWORD="" \
    MARIADB_ROOT_USER="root" \
    MYSQL_CLIENT_CREATE_DATABASE_NAME="" \
    MYSQL_CLIENT_CREATE_DATABASE_PASSWORD="" \
    MYSQL_CLIENT_CREATE_DATABASE_PRIVILEGES="ALL" \
    MYSQL_CLIENT_CREATE_DATABASE_USER="" \
    MYSQL_CLIENT_ENABLE_SSL="no" \
    MYSQL_CLIENT_SSL_CA_FILE="" \
    PATH="/opt/bitnami/php/bin:/opt/bitnami/php/sbin:/opt/bitnami/apache/bin:/opt/bitnami/common/bin:/opt/bitnami/mysql/bin:/opt/bitnami/magento/bin:$PATH"

EXPOSE 8080 8443

USER root
ENTRYPOINT [ "/opt/bitnami/scripts/magento/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/magento/run.sh" ]
