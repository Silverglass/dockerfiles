FROM buildpack-deps:stretch-scm

RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list \
    && sed -i 's|security.debian.org|mirrors.ustc.edu.cn/debian-security|g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
                       vim \
                       net-tools \
                       tcpdump \
                       nmap \
                       lsof \
                       telnet \
                       iptraf \
                       traceroute \
                       unzip \
                       xz-utils \
    && rm -rf /var/lib/apt/lists/*

ENV S6_OVERLAY_VERSION=v1.20.0.0 \
    S6_LOGGING_SCRIPT=n3\ s268435455 \
    S6_KEEP_ENV=1

RUN wget https://github.com/laincloud/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz -O /tmp/s6-overlay-amd64.tar.gz \
    && tar xvfz /tmp/s6-overlay-amd64.tar.gz -C / \
    && rm -f /tmp/s6-overlay-amd64.tar.gz

COPY rootfs /

ENTRYPOINT ["/app-init"]