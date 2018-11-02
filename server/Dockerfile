FROM centos:latest

MAINTAINER "Nguyen Trong Hieu" <tronghieudev@gmail.com>

ENV container docker

RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
 && rpm -Uvh https://rpms.remirepo.net/enterprise/remi-release-7.rpm

# normal updates
RUN yum -y update

# php && httpd
RUN yum -y install php70 php70-php php70-php-opcache php70-php-bcmath php70-php-cli php70-php-common php70-php-gd php70-php-intl php70-php-json php70-php-mbstring php70-php-pdo php70-php-pdo-dblib php70-php-pear php70-php-pecl-mcrypt php70-php-xmlrpc php70-php-xml php70-php-mysql php70-php-soap php70-php-pecl-zip php70-php-pecl-mongodb php70-php-pecl-xdebug php70-php-pecl-yaml httpd

# tools
RUN yum -y install epel-release iproute at curl crontabs git

# pagespeed
RUN curl -O https://dl-ssl.google.com/dl/linux/direct/mod-pagespeed-stable_current_x86_64.rpm \
 && rpm -U mod-pagespeed-*.rpm \
 && yum clean all \
 && php70 -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php70 composer-setup.php --install-dir=bin --filename=composer \
 && php70 -r "unlink('composer-setup.php');" \
 && rm -rf /etc/localtime \
 && ln -s /usr/share/zoneinfo/Europe/Berlin /etc/localtime \
 && ln -s /bin/php70 /bin/php

EXPOSE 80

COPY ./conf/welcome.conf /etc/httpd/conf.d/

RUN systemctl enable httpd \
 && systemctl enable crond

CMD ["/sbin/init"]