FROM centos:centos8

COPY shib.repo /etc/yum.repos.d

RUN yum install -y -q shibboleth.x86_64 \
 && yum clean all \
 && rm -rf /var/cache/yum

RUN sed -i 's|var/log/shibboleth.*|/proc/self/fd/1|' /etc/shibboleth/shibd.logger

RUN chown -R 1000 /etc/shibboleth \
 && chgrp -R root /etc/shibboleth \
 && chmod -R g+r /etc/shibboleth

RUN chown -R 1000 /var/run/shibboleth \
 && chgrp root /var/run/shibboleth \
 && chmod g+rw /var/run/shibboleth

RUN chown -R 1000 /var/cache/shibboleth \
 && chgrp root /var/cache/shibboleth \
 && chmod g+rw /var/cache/shibboleth

COPY inc-md-cert-mdq.pem /etc/shibboleth/
COPY idp-metadata.xml /etc/shibboleth/

USER 1000

CMD /usr/sbin/shibd -F -f -w 30