FROM ubuntu:latest

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    sudo \
    git \
    openssh-client \
    vim\
    python3-pip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip3 install --upgrade pip \
	&& pip3 install --no-cache-dir -r requirements.txt \
    && rm requirements.txt

ARG USERNAME=user
ARG GROUPNAME=$USERNAME
ARG UID=1000
ARG GID=1000
ARG PASSWORD=hogehoge
RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID -G sudo $USERNAME && \
    echo $USERNAME:$PASSWORD | chpasswd && \
    echo "$USERNAME   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER $USERNAME