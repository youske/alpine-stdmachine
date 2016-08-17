# Alpine Linux glibc with conda2

FROM frolvlad/alpine-glibc
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.stdmachine.description="alpine conda2 image" \
      com.stdmachine.vendor="stdmachine" \
      com.stdmachine.role="conda2 image"

ENV CONDA_BASE=/conda
ENV MINICONDA=Miniconda-latest-Linux-x86_64.sh
ENV CONDA_URL=https://repo.continuum.io/miniconda/${MINICONDA}
ENV CONDA_PACKAGE="virtualenv"
ENV PIP_PACKAGE="pytest pytest-xdist"

ENV PACKAGE='bash ca-certificates libstdc++ sudo' \
    DOWNLOAD_PACKAGE='wget git build-base musl-dev linux-headers' \
    LANG=C.UTF-8 \
    PATH=${CONDA_BASE}/bin:$PATH \
    WORK_DIR=/home/admin

# apk install
RUN apk upgrade --no-cache && \
    apk update --no-cache && \
    apk add --no-cache ${PACKAGE} && \
    apk add --no-cache ${DOWNLOAD_PACKAGE} -t buildpack

# entrykit install
RUN wget -q --no-check-certificate ${ENTRYKIT_DOWNLOAD} -O- | tar zx && \
    chmod +x /entrykit && mv /entrykit /usr/bin && /usr/bin/entrykit --symlink

# gosu
RUN wget -q --no-check-certificate ${GOSU_DOWNLOAD} -O /usr/bin/gosu && chmod +x /usr/bin/gosu

# s6-overlay
RUN tar zxf /tmp/s6-overlay-amd64.tar.gz -C /

# conda install
RUN wget -q --no-check-certificate ${CONDA_URL} && \
    bash /${MINICONDA} -b -p ${CONDA_BASE} && \
    ln -s ${CONDA_BASE}/bin/* /usr/local/bin/ && \
    rm -rf /root/.[acpw]* /${MINICONDA} ${CONDA_BASE}/pkgs/* && \
    conda update -q -y conda && conda install -y ${CONDA_PACKAGE} && \
    pip install -U ${PIP_PACKAGE} && \
    conda clean -itpsly

RUN apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*

# add admin user
RUN adduser -D -h /home/admin -s /bin/bash admin admin

# sudoers setting
RUN echo "admin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

WORKDIR ${WORK_DIR}
ENTRYPOINT ["switch","shell=/bin/bash","--","/init"]
CMD ["/bin/bash"]
