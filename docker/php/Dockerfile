FROM php:7.2-fpm
RUN apt-get update && apt-get install -y git cron \
	libjpeg-dev libpng-dev libfreetype6-dev lsb-release

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN "date"


# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-configure gd \
           --with-gd \
           --with-freetype-dir=/usr/include/ \
           --with-png-dir=/usr/include/ \
           --with-jpeg-dir=/usr/include/
#RUN docker-php-ext-install zip intl json fileinfo
RUN docker-php-ext-install gd iconv

#RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#    && docker-php-ext-install -j$(nproc) gd
#RUN docker-php-ext-install -j$(nproc) mcrypt
#RUN docker-php-ext-install -j$(nproc) ssh2
#RUN docker-php-ext-install -j$(nproc) mysqlnd
RUN docker-php-ext-install -j$(nproc) iconv
RUN docker-php-ext-install zip
#RUN apk update && apk add git
RUN git clone https://github.com/PmaControl/PmaControl.git pmacontrol
RUN cd pmacontrol && composer install
ADD config.json pmacontrol/config.json
WORKDIR /var/www/html/pmacontrol
RUN ./install -c config.json
