FROM node:18.10-bullseye

ARG RUBY_VERSION=2.7.8
ENV NPM_GLOBAL_PREFIX=/npm

WORKDIR /coco

ENV PATH $PATH:/root/.rbenv/bin:/root/.rbenv/shims

#RUN echo "deb [trusted=yes] http://archive.debian.org/debian/ jessie main contrib non-free" > /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y git curl libssl-dev libreadline-dev zlib1g-dev autoconf bison \
                       build-essential libyaml-dev libncurses5-dev \
                       libffi-dev libgdbm-dev sudo && \
    curl -sL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-installer | bash -

RUN echo '%node ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

RUN rbenv install ${RUBY_VERSION} && \
    rbenv global ${RUBY_VERSION}

RUN mkdir $NPM_GLOBAL_PREFIX && \
    npm config set prefix $NPM_GLOBAL_PREFIX --global

RUN chown -R node:node /npm
COPY . .
USER 1000
