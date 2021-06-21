FROM alpine

ARG TC_VERSION=12

ADD tce-load.patch /tmp/
RUN apk add --no-cache curl patch \
    && curl -SLO http://www.tinycorelinux.net/${TC_VERSION}.x/x86_64/release/distribution_files/rootfs64.gz \
    && mkdir rootfs64 \
    && cd rootfs64 \
    && gzip -dc ../rootfs64.gz | cpio -id \
    && rm -f ../rootfs64.gz \
    && cd usr/bin \
    && patch < /tmp/tce-load.patch \
    && cd ../.. \
    && rm -f /tmp/tce-load.patch \
    && tar cf - . | gzip -c > /tmp/rootfs64.tar.gz \
    && cd .. \
    && rm -rf rootfs64

CMD ["/bin/true"]