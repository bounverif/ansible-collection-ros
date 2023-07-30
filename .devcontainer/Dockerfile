FROM ros:humble

ENV LC_ALL="en_US.UTF-8"
ENV LC_CTYPE="en_US.UTF-8"
ENV LANG="en_US.UTF-8"
ENV LANGUAGE="en_US.UTF-8"

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
    sudo \
    git \
    make \
    tar curl wget zip unzip gnupg2 \
    python3-pip \
    openssh-client openssh-server \
    locales \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

RUN locale-gen --purge "en_US.UTF-8"
RUN dpkg-reconfigure --frontend noninteractive locales

RUN groupadd bouncmpe -g 1000 \
    && useradd -ms /bin/bash bouncmpe -g 1000 -u 1000 \
    && printf "bouncmpe:bouncmpe" | chpasswd \
    && printf "bouncmpe ALL= NOPASSWD: ALL\\n" >> /etc/sudoers

USER bouncmpe
WORKDIR /home/bouncmpe

RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install --user ansible ansible-lint

ENV PATH=/home/bouncmpe/.local/bin:$PATH
