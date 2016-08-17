# Alpine Linux standard

FROM youske/alpine-stdmachine:base
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine r image" \
      com.stdmachine.role="r image"

//github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/${ENTRYKIT_FILE}

ENV PATH=$PATH \
    PACKAGE='go go-cross go-tools' \
    BUILDPACK='wget ca-certificates'

RUN apk add ${PACKAGE} --no-cache && apk add ${BUILDPACK} --no-cache -t buildpack


# remove
RUN apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*
