FROM centos:centos7
MAINTAINER The CentOS Project <cloud-ops@centos.org>

# Labels consumed by Red Hat build service
LABEL Component="nginx" \
      Name="centos/nginx-180-centos7" \
      Version="1.8.0" \
      Release="1"

# Labels could be consumed by OpenShift
LABEL io.k8s.description="nginx [engine x] is an HTTP and reverse proxy server, a mail proxy server, and a generic TCP/UDP proxy server, originally written by Igor Sysoev." \
      io.k8s.display-name="nginx 1.8.0" \
      io.openshift.expose-services="80:http" \
      io.openshift.tags="nginx"

RUN yum -y install --setopt=tsflags=nodocs centos-release-scl-rh && \
    yum -y update --setopt=tsflags=nodocs && \
    yum -y install --setopt=tsflags=nodocs scl-utils rh-nginx18 && \
    yum clean all && \
    mkdir -p /usr/share/nginx/html


RUN apk update; \
    apk upgrade;
RUN docker-php-ext-install mysqli

