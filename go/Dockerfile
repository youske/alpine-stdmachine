# Alpine Linux standard

FROM youske/alpine-stdmachine:latest
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine standard image" \
      com.stdmachine.vendor="stdmachine" \
      com.stdmachine.role="baseimage"

ENV PATH=$PATH \
    WORK_DIR=/workdir \
    PACKAGE='go go-cross go-tools' \
    BUILDPACK='musl-dev linux-headers'

RUN apk add ${PACKAGE} --no-cache && apk add ${BUILDPACK} --no-cache -t buildpack

# remove
RUN apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*
