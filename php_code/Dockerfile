FROM php:7.4.2-fpm-alpine

RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.12/community" >> /etc/apk/repositories; \
echo 'http://dl-cdn.alpinelinux.org/alpine/v3.12/main' >> /etc/apk/repositories

# Update apt
RUN apk --no-cache update \
    && apk add 'gnu-libiconv-dev' --no-cache \
    --repository http://dl-cdn.alpinelinux.org/alpine/v3.12/community \
    --repository http://dl-cdn.alpinelinux.org/alpine/v3.12/main

RUN apk --no-cache update \
    && apk --no-cache upgrade \
    && apk add --no-cache \    
    # Packages
        mysql-client \
        php7-mysqli \
        php7-pdo \
        freetype \
        libpng \
        freetype-dev \
        libpng-dev \
        jpeg-dev \
        libjpeg \
        libjpeg-turbo-dev \
        wget \
        python3 \
        py3-pip \
        zlib-dev \
        ttf-freefont \
        fontconfig \
        xvfb \
        libxrender-dev \
        gettext \
        gettext-dev \
        libxml2-dev \
        autoconf \
        g++ \
        git \
        bash \
        make \
        libstdc++ \
        libxrender \
        libxext \
        libssl1.1 \
        libx11 \
        ca-certificates \
        oniguruma-dev \
        font-noto-khmer \
        zip libzip-dev zip \        
        imagemagick imagemagick-dev && \
    pecl install -f imagick  && \
    docker-php-ext-enable imagick  && \
    apk del --purge autoconf g++ make
RUN apk add --no-cache icu-dev

RUN python3 -m pip install --upgrade pip

RUN docker-php-ext-configure gd --with-freetype --with-jpeg

RUN docker-php-ext-install zip
RUN docker-php-ext-install opcache
RUN docker-php-ext-install gettext
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install xml
RUN docker-php-ext-install iconv 
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install intl

RUN  rm -rf /var/www/html \
    && ln -s /var/www/symfony/public /var/www/html

WORKDIR /var/www/symfony

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN git config --global user.email "erwin.macaraig@gmail.com" \ 
    && git config --global user.name "Erwin"