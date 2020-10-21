# CEKit is only supported on RHEL 7
FROM registry.access.redhat.com/ubi7/ubi-minimal:7.8

# CEKit requires epl-release repository
RUN rpm -i https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

# Install CEKit, Buildah and Git
RUN microdnf install --nodocs --enablerepo=rhel-7-server-rpms --enablerepo=rhel-7-server-extras-rpms \
    buildah \
    git \
    cekit \
    && microdnf clean all