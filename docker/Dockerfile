FROM ppoffice/mssql-odbc

RUN apt-get update && \
    apt-get -y install apache2 php5 php5-mssql && \
    apt-get -y install php5-curl && \
    apt-get -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY configs/php.ini /etc/php5/apache2/php.ini
COPY configs/000-default.conf /etc/apache2/sites-available/

RUN  a2enmod rewrite && \
     php5enmod mssql


RUN echo "ServerName localhost" >> /etc/apache2/httpd.conf && \
    echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Uncomment these two lines to fix "non-UTF8" chars encoding and time format problems
 ADD configs/freetds.conf /etc/freetds/
 ADD configs/locales.conf /etc/freetds/
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]