FROM centos:centos8

COPY shib.repo /etc/yum.repos.d

RUN yum install -y -q httpd shibboleth \
 && yum clean all \
 && rm -rf /var/cache/yum

RUN chown -R 1000 /etc/shibboleth \
 && chgrp -R root /etc/shibboleth \
 && chmod -R g+r /etc/shibboleth

RUN chown -R 1000 /var/run/shibboleth \
 && chgrp root /var/run/shibboleth \
 && chmod g+rw /var/run/shibboleth

COPY index.html /var/www/html/index.html
COPY shib.conf /etc/httpd/conf.d

EXPOSE 80
EXPOSE 443

# CMD rm -rf /run/httpd/* /tmp/httpd* && exec httpd -DFOREGROUND
CMD exec httpd -DFOREGROUND