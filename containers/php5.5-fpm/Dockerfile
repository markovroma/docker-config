FROM php:5.5-fpm
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        php-calendar \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) pdo pdo_mysql calendar
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/xdebug.ini \ 
    && echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.idekey=xdebug" >> /usr/local/etc/php/conf.d/xdebug.ini \ 
    && echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/xdebug.ini 
COPY ./config/php.ini /usr/local/etc/php/php.ini

RUN apt-get update && apt-get install -y wget dpkg 
RUN wget http://security.ubuntu.com/ubuntu/pool/main/libj/libjpeg-turbo/libjpeg-turbo8_1.1.90+svn733-0ubuntu4.3_amd64.deb
RUN dpkg -i libjpeg-turbo8_1.1.90+svn733-0ubuntu4.3_amd64.deb
RUN apt-get install -y libxrender1 xfonts-75dpi xfonts-base fontconfig libx11-6 libxext6  
RUN wget http://packages.rusoft.ru/ppa/wkhtmltopdf/pool/ubuntu-trusty/amd64/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
RUN dpkg -i wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
RUN apt-get install -y xvfb
COPY ./config/wkhtmltopdf.sh /usr/local/bin/wkhtmltopdf.sh
RUN chmod +x /usr/local/bin/wkhtmltopdf.sh

RUN apt-get install -y \
 software-properties-common \ 
 python-software-properties
RUN \
echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
apt-get update && \
apt-get install -y oracle-java8-installer && \
update-alternatives --config java

