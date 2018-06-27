FROM php:7.2-fpm
# -alpine
#RUN apk --update --no-cache add \
#	lsb_release \
#	unzip \
#	icu-dev \
#	g++ \
#	freetype-dev \
#	libjpeg-turbo-dev \
#	libpng-dev \
#	libcurl \
#	bash \
#	bash-completion \
#	yaml \
#	nano \
#	tar \
#	make \
#	libffi-dev \
#	ruby ruby-irb ruby-rake ruby-io-console ruby-bigdecimal ruby-json ruby-bundler
RUN apt-get update && apt-get install -y git \
	libjpeg-dev libpng-dev libfreetype6-dev lsb-release
#libjpeg-turbo8
#	ruby-dev ruby-rdoc \
#	curl-dev \
#	libstdc++ tzdata ca-certificates \
#	&& gem install sass --no-user-install

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
RUN cd pmacontrol && ./install -c config.json
