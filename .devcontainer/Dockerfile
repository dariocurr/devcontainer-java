# for format details, see https://docs.docker.com/engine/reference/builder/

ARG VARIANT="11"

# select image
FROM mcr.microsoft.com/vscode/devcontainers/java:${VARIANT}
LABEL author="dariocurr@gmail.com" maintainer="dariocurr@gmail.com" version="0.0.1"

# update apt
RUN apt -qq update \
    && apt -qq upgrade -y \
    && export DEBIAN_FRONTEND=noninteractive

# install Maven or Gradle
ARG INSTALL_MAVEN="true"
ARG MAVEN_VERSION="3.6.3"
ARG INSTALL_GRADLE="false"
ARG GRADLE_VERSION=""
RUN if [ "${INSTALL_MAVEN}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install maven \"${MAVEN_VERSION}\""; fi \
    && if [ "${INSTALL_GRADLE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install gradle \"${GRADLE_VERSION}\""; fi

# read and change user
ARG USER="vscode"
USER ${USER}

# add zsh configuration and replace oh-my-zsh with antigen
WORKDIR /home/${USER}/
RUN rm -r .oh-my-zsh; \
    git clone -q https://github.com/zsh-users/antigen.git .antigen;
ADD --chown=${USER} https://gist.githubusercontent.com/dariocurr/9792ae1fb6ddf736d8fea9e20eb13e26/raw/ .zshrc