FROM php:5.6-fpm

# install the PHP extensions we need
RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev git && rm -rf /var/lib/apt/lists/* \
        && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
        && docker-php-ext-install gd
RUN docker-php-ext-install mysqli

WORKDIR /var/www/html

ENV JOOMLA_VERSION 3.4.3
ENV JOOMLA_SHA1 9f4e983c6a11ba137bfd5c4355764a754d7e9497
ENV JOOMLA_URL https://github.com/joomla/joomla-cms/releases/download/${JOOMLA_VERSION}/Joomla_${JOOMLA_VERSION}-Stable-Full_Package.tar.gz

RUN curl -o joomla.tar.gz -SL ${JOOMLA_URL} \
	&& echo "$JOOMLA_SHA1 joomla.tar.gz" | sha1sum -c - \
	&& tar -xzf joomla.tar.gz -C /var/www/html/ \
	&& rm joomla.tar.gz \
	&& chown -R www-data:www-data /var/www/html

VOLUME /var/www/html

RUN mkdir /var/www/pimp \
  && git clone https://github.com/potsky/PimpMyLog.git /var/www/pimp \
  && chown -R www-data:www-data /var/www/pimp
  && cp /var/www/pimp/cfg/config.example.php /var/www/pimp/config.user.php

VOLUME /var/www/pimp

CMD ["php-fpm"]
