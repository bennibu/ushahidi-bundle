FROM php:7.1-apache-stretch

RUN apt-get update && \
  apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmcrypt-dev \
    libc-client2007e-dev \
    libkrb5-dev \
    libcurl4-openssl-dev \
    unzip \
    rsync \
    git \
    netcat && \
  docker-php-ext-install curl json mcrypt bcmath pdo pdo_mysql mysqli && \
  docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
  docker-php-ext-install imap && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install gd && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl -sS https://getcomposer.org/installer | \
      php -- --install-dir=/usr/local/bin --filename=composer

ENV VERSION v3.7.1
RUN git clone https://github.com/ushahidi/platform.git \
      /var/www/html && \
  cd /var/www/html && \
  git checkout tags/$VERSION && \
  git checkout -b deploy && \
  mv httpdocs/template.htaccess httpdocs/.htaccess && \
  chmod 0777 application/logs application/cache application/media/uploads && \
  sed -i 's/var\/www\/html/var\/www\/html\/httpdocs/' /etc/apache2/sites-available/000-default.conf && \
  a2enmod rewrite && \
  ./bin/update --production --no-migrate

