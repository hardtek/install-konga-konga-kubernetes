FROM bitnami/kong:2.8.0

USER root

RUN mkdir certificado-ipp

RUN apt -y update && apt -y upgrade

COPY gitlab.ipirangacloud.com.crt /certificado-ipp
COPY gitlab.ipirangacloud.com.key /certificado-ipp

RUN \
 apt -y install \
#   --virtual build-dependencies \
#    build-base \
   gcc \
   wget \
   git \
   ruby 
   # openssl-dev \
   # libuuid \
   # yaml-dev

RUN luarocks install kong-plugin-amqp

RUN ls -la 

RUN ls -la /opt/bitnami/kong/openresty/luajit/share/lua/5.1/kong/plugins

# This is required because this plugin needs to write a kong core file
# Issue #8 https://github.com/gsdenys/kong-plugin-amqp/issues/8
RUN /opt/bitnami/kong/openresty/luajit/bin/luajit /opt/bitnami/kong/openresty/luajit/share/lua/5.1/kong/plugins/amqp/prepare.lua

USER 1001