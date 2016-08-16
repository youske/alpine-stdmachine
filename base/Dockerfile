# Alpine Linux standard base image

FROM alpine:latest
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine standard image" \
      com.stdmachine.role="baseimage"

# s6-overlay
ENV S6OVERLAY_VERSION="v1.11.0.1"
ENV S6OVERLAY_URL="https://github.com/just-containers/s6-overlay/releases/download/${S6OVERLAY_VERSION}/s6-overlay-amd64.tar.gz"
ADD ${S6OVERLAY_URL} /tmp/

ENV ENTRYKIT_VERSION=0.4.0
ENV ENTRYKIT_FILE=entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz
ENV ENTRYKIT_DOWNLOAD=https://github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/${ENTRYKIT_FILE}
ADD ${ENTRYKIT_DOWNLOAD} /tmp/

ENV GOSU_VERSION=1.7
ENV GOSU_DOWNLOAD=https://github.com/tianon/gosu/releases/download/${GOSU_VERSION}/gosu-amd64
ADD ${GOSU_DOWNLOAD} /usr/bin/

ENV LC_ALL=C.UTF-8
ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=${LANG}

ENV PACKAGE='bash wget python ca-certificates' \
    BUILDPACK='git build-base musl-dev linux-headers' \
    PATH=$PATH \
    WORK_DIR=/workdir


# timezone settings
ENV TZ=Asia/Tokyo
RUN apk --update add tzdata && \
    cp /usr/share/zoneinfo/${TZ} /etc/localtime && echo $TZ > /etc/timezone && \
    apk del tzdata


# package install & update
RUN echo "http://dl-3.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN apk update upgrade --no-cache && \
    apk add ${PACKAGE} --no-cache && \
    apk add ${BUILDPACK} --no-cache -t buildpack

# entrykit install
RUN tar zxf /tmp/${ENTRYKIT_FILE} -C /usr/bin && \
    chmod +x /usr/bin/entrykit && /usr/bin/entrykit --symlink

# gosu
RUN  chmod +x /usr/bin/gosu-amd64 && ln -s /usr/bin/gosu-amd64 /usr/bin/gosu

# s6-overlay
RUN tar zxf /tmp/s6-overlay-amd64.tar.gz -C /

# admin user
RUN adduser -D -h /home/admin -s /bin/bash admin admin

# pre installed package remove
RUN apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*

RUN mkdir -p ${WORK_DIR}

WORKDIR ${WORK_DIR}
ENTRYPOINT ["switch","shell=/bin/bash","--","/init"]
CMD ["gosu","admin","/bin/bash"]
