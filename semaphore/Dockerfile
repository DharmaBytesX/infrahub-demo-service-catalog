FROM semaphoreui/semaphore:v2.17.12

USER root

RUN apk add --no-cache python3 py3-pip && \
    pip3 install --break-system-packages infrahub-sdk

USER semaphore
RUN mkdir -p /opt/semaphore/collections
RUN ansible-galaxy collection install opsmill.infrahub -p /opt/semaphore/collections

# The playbooks, so a Semaphore without the repository mounted (a public sandbox) can run them.
# The local stack mounts ./ansible over this folder, so local edits apply without a rebuild.
COPY --chown=semaphore ansible/ /opt/semaphore/playbooks/
