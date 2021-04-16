FROM naqoda/centos-apache-php
COPY php.ini /etc/
COPY vhost-ssl.conf /etc/httpd/conf.d/
COPY vhost.conf /etc/httpd/conf.d/
RUN yum -y install git
RUN curl -Lsf 'https://golang.org/dl/go1.15.2.linux-amd64.tar.gz ' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' >> /etc/php.ini