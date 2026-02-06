FROM quay.io/centos/centos:stream9

ENV container docker

# Install systemd and RHCSA tools
RUN dnf -y install \
    systemd systemd-libs systemd-udev \
    vim man-pages man-db \
    net-tools iproute \
    util-linux \
    lvm2 \
    tar \
    && dnf clean all

# Needed for systemd inside container
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/sbin/init"]
