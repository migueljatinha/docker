FROM php:7.3-fpm
LABEL Caique Galvanin Rodrigues <caique.galvanin@gmail.com>
# PREPARE ENVIRONMENT

RUN  	apt-get update && apt-get install -y \
		wget \
		libzip-dev \
		zip \
		git \
		vim \
		libmcrypt-dev \
		libfreetype6-dev \
		build-essential \
		libssh2-1 \
		libssh2-1-dev \
		libxslt-dev	\
		libxml2-dev \
		libjpeg62-turbo-dev libpng-dev libxpm-dev \
		libfreetype6-dev \
		procps

# INSTALL EXTENSIONS
RUN		docker-php-ext-install pdo_mysql soap mysqli bcmath sockets sysvsem mbstring
RUN 	docker-php-ext-install -j$(nproc) iconv
RUN 	pecl install xdebug && docker-php-ext-enable xdebug
RUN 	docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install -j$(nproc) gd
RUN 	curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

RUN apt-get update \
	  && apt-get install -y zlib1g-dev libicu-dev g++ wkhtmltopdf xvfb \
	  && docker-php-ext-configure intl \
	  && docker-php-ext-install intl \
	  && docker-php-ext-configure pcntl \
	  && docker-php-ext-install pcntl \
	  && docker-php-ext-configure zip \
	  && docker-php-ext-install zip \
	  && docker-php-ext-install xsl \
	  && docker-php-ext-install exif \
	  && docker-php-ext-install gettext \
	  && docker-php-ext-install calendar

RUN docker-php-ext-install calendar
RUN apt install -y jq

#mysql
RUN apt-get install -y mariadb-client

# CREATE PROJECT DIRECTORIES
RUN 	useradd -u 1000 -G root,www-data -s /bin/bash master \
	&& usermod -a -G master www-data \
	&& usermod -s /bin/bash www-data
WORKDIR /home/master
RUN chmod -R 777 /home/master