FROM centos:7

COPY cloudkeeper.repo /etc/yum.repos.d/cloudkeeper.repo

# hadolint ignore=DL3033
RUN yum install -y centos-release-openstack-stein \
    && yum install -y cloudkeeper-os \
    && yum clean all

RUN mkdir -p /etc/cloudkeeper-os/ \
             /var/spool/cloudkeeper/images

COPY cloudkeeper-os.conf /etc/cloudkeeper-os/cloudkeeper-os.conf
COPY mapping.json /etc/cloudkeeper-os/mapping.json

# Patch the cloudkeeper-os
COPY openstack_client.py /usr/lib/python2.7/site-packages/cloudkeeper_os/openstack_client.py
RUN python -m compileall  /usr/lib/python2.7/site-packages/cloudkeeper_os/openstack_client.py

EXPOSE 50051

CMD ["cloudkeeper-os"]
