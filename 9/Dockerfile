FROM registry.access.redhat.com/ubi9/ubi:latest

LABEL maintainer="mullholland"
LABEL build_update="2023-05-22"

ENV container=docker

# Silence annoying subscription messages.
RUN echo "enabled=0" >> /etc/yum/pluginconf.d/subscription-manager.conf

# Install systemd -- See https://hub.docker.com/_/centos/
RUN yum -y update; yum clean all; \
  cd /lib/systemd/system/sysinit.target.wants/ ; \
  for i in * ; do [ $i = systemd-tmpfiles-setup.service ] || rm -f $i ; done ; \
  rm -f /lib/systemd/system/multi-user.target.wants/* ; \
  rm -f /etc/systemd/system/*.wants/* ; \
  rm -f /lib/systemd/system/local-fs.target.wants/* ; \
  rm -f /lib/systemd/system/sockets.target.wants/*udev* ; \
  rm -f /lib/systemd/system/sockets.target.wants/*initctl* ; \
  rm -f /lib/systemd/system/basic.target.wants/* ; \
  rm -f /lib/systemd/system/anaconda.target.wants/*

# Install requirements.
RUN yum makecache --timer \
 && yum -y install initscripts \
 && yum -y update \
 && yum -y install \
      sudo \
      which \
      hostname \
      procps-ng \
      ca-certificates \
      iproute \
 && yum clean all

# Disable requiretty.
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers


VOLUME ["/sys/fs/cgroup"]

CMD ["/usr/lib/systemd/systemd"]
