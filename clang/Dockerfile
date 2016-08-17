# Alpine Linux clang

FROM youske/alpine-stdmachine:base
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine clang image" \
      com.stdmachine.role="clang image"

RUN apk add gcc g++ clang --no-cache && \
    rm -rf /tmp/* /var/cache/apk/*
