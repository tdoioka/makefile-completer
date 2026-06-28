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
    bash-completion \
    ;

# install from not apt packages
RUN export DEBIAN_FRONTEND=noninteractive; \
    # Define tempolary packages for setup.
    # curl and avoid error in curl packages (locales-all and ca-certificates).
    PKGS_FOR_SETUP_CONTAINER=( \
        curl \
        locales-all \
    ); \
    # install tempolary pacakges for setup.
    apt-get update && apt-get install -y --no-install-recommends \
        ca-certificates \
        ${PKGS_FOR_SETUP_CONTAINER[@]}; \
    # update repository list for nodejs
    curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -; \
    apt-get update && apt-get install -y --no-install-recommends \
        nodejs \
        ; \
    # remove templary packages for setup.
    apt remove --purge -y \
        ${PKGS_FOR_SETUP_CONTAINER[@]}; \
    apt autopurge -y; \
    :;

# when ubuntu is not exists create ubuntu user
# Ubuntu 24.04 or later built in user ubuntu(uid=1000,gid=1000).
RUN user=ubuntu; \
    if ! id "$user"; then \
        useradd -m -G sudo -s /bin/bash -u 1000 "$user"; \
    fi; \
    echo ubuntu:ubuntu | chpasswd

ENV GIT_COMPLETION_SHOW_ALL=1

# USER ubuntu
