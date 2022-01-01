FROM php:7.4-fpm AS sap
ADD nwrfcsdk.tar.gz /usr/sap/
RUN apt-get update && apt-get install -y git-core
WORKDIR /usr/local/src/
RUN git clone https://github.com/gkralik/php7-sapnwrfc.git
WORKDIR /usr/local/src/php7-sapnwrfc
RUN phpize
RUN ./configure
RUN make
RUN find /usr/local/src/php7-sapnwrfc

FROM php:7.4-fpm
ADD nwrfcsdk.tar.gz /usr/sap/
COPY --from=sap /usr/local/src/php7-sapnwrfc/modules/sapnwrfc.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions calendar exif gd gettext intl mysqli pdo_mysql shmop soap sockets xsl zip pcntl sysvmsg sysvsem sysvshm opcache

ADD conf/ /usr/local/etc/php/conf.d/
