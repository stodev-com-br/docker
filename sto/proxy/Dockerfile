FROM ubuntu:16.04

LABEL maintainer="Geverson R. Sarmento <geverson.sarmento@stodev.com.br>"
SHELL ["/bin/bash", "-c"]

RUN apt-get update
RUN apt-get install apt-utils -y
RUN apt-get upgrade -y 
RUN apt-get install apache2 apache2-utils -y
RUN a2enmod ssl proxy

RUN touch /var/log/apache2/apache2.log
COPY apache2/conf-available/server-name.conf /etc/apache2/conf-available/server-name.conf
COPY apache2/conf-available/googleapis.conf /etc/apache2/conf-available/googleapis.conf
RUN a2enconf server-name googleapis

COPY apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
RUN a2ensite 000-default default-ssl

WORKDIR /var/www/html

EXPOSE 80 443

CMD ["/bin/bash", "-c", "apachectl start && tail -f /var/log/apache2/apache2.log" ]