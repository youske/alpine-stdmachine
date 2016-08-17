# Alpine Linux with nodejs

FROM youske/alpine-stdmachine:base
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine nodejs image" \
      com.stdmachine.vendor="stdmachie" \
      com.stdmachine.role="nodejs image"

COPY package.json /tmp/package.json

RUN apk update upgrade --no-cache && \
    apk add nodejs --no-cache && \
    apk add build-base linux-headers musl-dev nodejs-dev --no-cache -t buildpack && \
    cd /tmp && npm install -g && \
    apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*
