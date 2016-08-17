# Alpine Linux go

FROM youske/alpine-stdmachine:base
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine go image" \
      com.stdmachine.vendor="stdmachine" \
      com.stdmachine.role="go image"

RUN apk add go go-cross go-tools --no-cache && \
    rm -rf /tmp/* /var/cache/apk/*
