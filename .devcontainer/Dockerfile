# for format details, see https://docs.docker.com/engine/reference/builder/

# select image
# see here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.195.0/containers/java/.devcontainer/base.Dockerfile
ARG JAVA_VERSION="11-bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/java:0-${JAVA_VERSION}
LABEL author="dariocurr@gmail.com" maintainer="dariocurr@gmail.com" version="0.0.1"

# update apt
RUN apt update \
    && apt upgrade -y \
    && export DEBIAN_FRONTEND=noninteractive

# install Maven or Gradle
ARG INSTALL_MAVEN="true"
ARG MAVEN_VERSION="3.6.3"
ARG INSTALL_GRADLE="false"
ARG GRADLE_VERSION=""
RUN if [ "${INSTALL_MAVEN}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install maven \"${MAVEN_VERSION}\""; fi \
    && if [ "${INSTALL_GRADLE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install gradle \"${GRADLE_VERSION}\""; fi

# add zsh configuration and replace oh-my-zsh with antigen
USER vscode
WORKDIR /home/vscode/
RUN rm -r .oh-my-zsh \
    && git clone https://github.com/zsh-users/antigen.git .antigen
COPY .devcontainer/.zshrc .