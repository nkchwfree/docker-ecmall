FROM php:5.5.28-fpm


# RUN gpg --recv-keys AA8E81B4331F7F50 && gpg --export AA8E81B4331F7F50 | apt-key add - \
#    && rm -rvf /var/lib/apt/lists/* \
RUN echo "deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib" > /etc/apt/sources.list \
    && echo "deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib"  >> /etc/apt/sources.list \
    && apt-get update --fix-missing;exit 0 

RUN apt-get install -y g++ autoconf bash apt-utils libxml2-dev libcurl3-dev pkg-config zlib1g-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && pecl install redis-4.3.0 \    
    && docker-php-ext-enable redis \
    && docker-php-ext-install iconv curl mbstring xml json mysql mysqli pdo pdo_mysql zip \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-enable gd \
    && apt-get purge -y --auto-remove \
    && rm -rf /var/cache/apt/* \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /pecl
