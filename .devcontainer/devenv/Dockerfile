ARG CONTAINER_BASE=amd64/ubuntu:22.04

FROM ${CONTAINER_BASE}
SHELL ["/bin/bash","-xueo","pipefail","-c"]

# requirement tools instration.
RUN export DEBIAN_FRONTEND=noninteractive; \
    apt-get update && apt-get install -y --no-install-recommends \
    sudo \
    git \
    openssh-client \
    make \
    ;

# when ubuntu is not exists create ubuntu user
# Ubuntu 24.04 or later built in user ubuntu(uid=1000,gid=1000).
RUN user=ubuntu; \
    if ! id "$user"; then \
        useradd -m -G sudo -s /bin/bash -u 1000 "$user"; \
    fi; \
    echo ubuntu:ubuntu | chpasswd

# USER ubuntu
