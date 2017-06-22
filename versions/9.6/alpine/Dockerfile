#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "./hack/run update"
#
# DO NOT EDIT IT DIRECTLY.
#
FROM postgres:9.6-alpine
# <pre>

MAINTAINER AusNimbus <support@ausnimbus.com.au>

LABEL summary="Platform for running PostgreSQL 9.6 applications" \
      maintainer="AusNimbus <support@ausnimbus.com.au>" \
      io.k8s.description="Platform for running PostgreSQL 9.6 applications" \
      io.k8s.display-name="PostgreSQL 9.6"

ENV USER=100 \
    HOME=/opt/app-root/src

USER 0

RUN apk --no-cache add bash rsync && \
    ln -sf /bin/bash /bin/sh && \
    mkdir -p $HOME && \
    adduser -S -u 1001 -G root -h $HOME -s /sbin/nologin \
      -g "Default Application User" default && \
    chown -R 1001:0 /opt/app-root

# Copy common executable utilities.
COPY ./common/bin/ /usr/bin/

# Each container image can have 'contrib' a directory with extra files needed to
# run and build the application.
COPY ./contrib/ /opt/app-root

# </pre>
# <component>

# Copy the component scripts (override existing container-entrypoint)
COPY ./component/bin/ /usr/bin/

# </component>
# <template>

LABEL io.openshift.expose-services="5432:tcp" \
    io.openshift.tags="component,postgres"

# </template>
# <post>

# Standardize on UID $USER (alpine:3.4 does not have the shadow package)
RUN apk add shadow --no-cache --repository http://rsync.alpinelinux.org/alpine/latest-stable/community/ && \
    usermod -o -u $USER default && \
    apk del shadow

# Drop the root user and make the content of /opt/app-root owned by user default
RUN chown -R $USER:0 /opt/app-root && chmod -R ug+rwx /opt/app-root
USER $USER

ENTRYPOINT ["container-entrypoint"]

# </post>
