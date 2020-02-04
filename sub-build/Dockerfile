FROM registry.redhat.io/rhel7
#Copy entitlements and certificates from created secrets
COPY ./etc-pki-entitlement /etc/pki/entitlement
COPY ./rhsm-conf /etc/rhsm
COPY ./rhsm-ca /etc/rhsm/ca
RUN rm /etc/rhsm-host && yum repolist --disablerepo=* && subscription-manager repos --enable rhel-7-server-rpms && yum -y install httpd && yum clean all

RUN sed -i 's/Listen 80/Listen 8080/'  /etc/httpd/conf/httpd.conf  && chgrp -R 0 /var/log/httpd /var/run/httpd  && chmod -R g=u /var/log/httpd /var/run/httpd && echo "Azure Red Hat OpenShift" > /var/www/html/index.html
EXPOSE 8080
USER 1001
CMD /usr/sbin/httpd -D FOREGROUND
