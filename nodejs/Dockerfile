# Alpine Linux with nodejs

FROM youske/alpine-stdmachine:latest
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine nodejs image" \
      com.stdmachine.vendor="stdmachie" \
      com.stdmachine.role="baseimage"

ENV PATH=$PATH \
    PACKAGE='nodejs' \
    BUILDPACK='build-base linux-headers musl-dev nodejs-dev'

COPY package.json /tmp/package.json

RUN apk update upgrade --no-cache && \
    apk add ${PACKAGE} --no-cache && \
    apk add ${BUILDPACK} --no-cache -t buildpack && \
    cd /tmp && npm install -g && \
    apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*
