# Alpine Linux with nodejs

FROM youske/alpine-stdmachine:latest
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine nodejs image" \
      com.stdmachine.role="baseimage"

ENV PATH=$PATH \
    LANG=C.UTF-8 \
    WORK_DIR=/home/admin \
    PACKAGE='bash nodejs ca-certificates' \
    BUILDPACK='wget build-base linux-headers musl-dev git nodejs-dev'

RUN adduser -D -h /home/admin -s /bin/bash admin admin

RUN apk update upgrade --no-cache && \
    apk add ${PACKAGE} --no-cache && \
    apk add ${BUILDPACK} --no-cache -t buildpack

COPY package.json /tmp/package.json
RUN cd /tmp && npm install -g
# gulp pm2 forever

RUN apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*
