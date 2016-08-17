FROM youske/alpine-stdmachine:base
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine python2 image" \
      com.stdmachine.vendor="stdmachine" \
      com.stdmachine.role="python2 image"

RUN apk add --no-cache python && \
    python -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip install --upgrade pip setuptools && \
    rm -r /root/.cache
