# Alpine Linux standard base image

FROM alpine:3.4
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine standard image" \
      com.stdmachine.vendor="stdmachine" \
      com.stdmachine.role="baseimage"

# s6-overlay
ENV S6OVERLAY_VERSION="v1.11.0.1"
ADD https://github.com/just-containers/s6-overlay/releases/download/${S6OVERLAY_VERSION}/s6-overlay-amd64.tar.gz /tmp/

ENV ENTRYKIT_VERSION=0.4.0
ENV ENTRYKIT_FILE=entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz
ADD https://github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/${ENTRYKIT_FILE} /tmp/

ENV GOSU_VERSION=1.7
ADD https://github.com/tianon/gosu/releases/download/${GOSU_VERSION}/gosu-amd64 /usr/bin/

ENV LC_ALL=C.UTF-8
ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=${LANG}

ENV PATH=${PATH} \
    WORK_DIR=/workdir

# timezone settings
ENV TZ=Asia/Tokyo
RUN apk --update add tzdata && \
    cp /usr/share/zoneinfo/${TZ} /etc/localtime && echo $TZ > /etc/timezone && \
    apk del tzdata

# package install & update
RUN echo "http://dl-3.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk update upgrade --no-cache && \
    apk add bash git wget ca-certificates --no-cache

# docker support install
RUN tar zxf /tmp/${ENTRYKIT_FILE} -C /usr/bin && \
    chmod +x /usr/bin/entrykit && /usr/bin/entrykit --symlink && \
    chmod +x /usr/bin/gosu-amd64 && ln -s /usr/bin/gosu-amd64 /usr/bin/gosu && \
    tar zxf /tmp/s6-overlay-amd64.tar.gz -C /

RUN \
  # pre installed package remove
  rm -rf /tmp/* /var/cache/apk/* && \
  # admin user & work
  adduser -D -h /home/admin -s /bin/bash admin admin && \
  mkdir -p ${WORK_DIR}

WORKDIR ${WORK_DIR}
ENTRYPOINT ["switch","shell=/bin/bash","--","/init"]
CMD ["gosu","admin","/bin/bash"]
