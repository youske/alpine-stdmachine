# Alpine Linux standard

FROM youske/alpine-stdmachine:nodejs
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.geeplus.description="alpine standard image" \
      com.geeplus.vendor="geeplus.inc" \
      com.geeplus.role="baseimage"

# s6-overlay
ENV S6OVERLAY_VERSION="v1.11.0.1"
ENV S6OVERLAY_URL="https://github.com/just-containers/s6-overlay/releases/download/${S6OVERLAY_VERSION}/s6-overlay-amd64.tar.gz"
ADD ${S6OVERLAY_URL} /tmp/


ENV ENTRYKIT_VERSION=0.4.0
ENV ENTRYKIT_FILE=entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz
ENV ENTRYKIT_DOWNLOAD=https://github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/${ENTRYKIT_FILE}

ENV PATH=$PATH \
    LANG=C.UTF-8 \
    WORK_DIR=/home/admin \
    PACKAGE='go go-cross go-tools' \
    BUILDPACK='wget ca-certificates'

RUN apk add ${PACKAGE} --no-cache && apk add ${BUILDPACK} --no-cache -t buildpack

# entrykit install
RUN wget -q --no-check-certificate ${ENTRYKIT_DOWNLOAD} -O- | tar zx && \
    chmod +x /entrykit && mv /entrykit /bin && /bin/entrykit --symlink

# gosu

# remove
RUN apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*

RUN adduser -D -h /home/admin -s /bin/bash admin admin

WORKDIR ${WORK_DIR}
ENTRYPOINT ["switch","shell=/bin/bash","--","/bin/bash"]
