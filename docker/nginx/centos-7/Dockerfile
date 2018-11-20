# Labels consumed by Red Hat build service
#docker build -t nginx .

FROM centos:centos7
MAINTAINER The CentOS Project <cloud-ops@centos.org>

ENV WEB_DOCUMENT_ROOT=/app \
    WEB_DOCUMENT_INDEX=index.php \
    WEB_ALIAS_DOMAIN=*.vm \
    WEB_PHP_TIMEOUT=600 \
    WEB_PHP_SOCKET=""
ENV WEB_PHP_SOCKET=127.0.0.1:9000

COPY conf/ /opt/docker/

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

RUN set -x \
    # Install apache
    && yum-install \
        httpd \
        mod_ssl \
    && sed -ri ' \
        s!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g; \
        s!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g; \
        ' /etc/httpd/conf/httpd.conf /etc/httpd/conf.d/ssl.conf \
    && docker-run-bootstrap \
    && docker-image-cleanup

# Get prefix path and path to scripts rather than hard-code them in scripts

COPY conf/ /opt/docker/

# ADD https://git.centos.org/sources/httpd/c7/acf5cccf4afaecf3afeb18c50ae59fd5c6504910 /usr/share/nginx/html/
# RUN sed -i -e 's/Apache/nginx/g' -e '/apache_pb.gif/d' /usr/share/nginx/html/index.html
RUN echo "nginx on CentOS7" > /usr/share/nginx/html/index.html

EXPOSE 80 443

USER nginx

ENTRYPOINT ["container-entrypoint"]
CMD [ "nginx18" ]

