ARG CONTRAIL_REGISTRY
ARG CONTRAIL_CONTAINER_TAG
FROM ${CONTRAIL_REGISTRY}/contrail-base:${CONTRAIL_CONTAINER_TAG}
ARG VENDOR_DOMAIN

ARG CONTAINER_NAME
LABEL name=$CONTAINER_NAME \
      summary="Ironic Notification Manager for OpenStack" \
      description="OpenStack bare metal provisioning a.k.a Ironic is an integrated OpenStack program which aims to provision bare metal machines instead of virtual machines, forked from the Nova baremetal driver."

RUN yum install -y ironic-notification-manager && \
    yum clean all -y && \
    rm -rf /var/cache/yum

COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]
CMD ["/usr/bin/ironic-notification-manager", "--conf_file", "/etc/contrail/ironic-notification-manager.conf", "--conf_file", "/etc/contrail/contrail-keystone-auth.conf"]

ENV NODE_TYPE=openstack
LABEL $VENDOR_DOMAIN".pod"=$NODE_TYPE

ENV SERVICE_NAME=ironic
LABEL $VENDOR_DOMAIN".service"=$SERVICE_NAME
LABEL $VENDOR_DOMAIN".container.name"=$CONTAINER_NAME
