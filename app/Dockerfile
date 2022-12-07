FROM --platform=linux/amd64 naqoda/centos-apache-php:latest
RUN yum -y install git
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.19.4.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go install github.com/mailhog/mhsendmail@v0.2.0
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
COPY php.ini /etc/
COPY vhost-ssl.conf /etc/httpd/conf.d/
COPY vhost.conf /etc/httpd/conf.d/
RUN echo "sendmail_path = '/usr/bin/mhsendmail --smtp-addr=mailhog:1025'" >> /etc/php.ini