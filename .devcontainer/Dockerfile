# select image
ARG JAVA_VERSION="11-bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/java:0-${JAVA_VERSION}
LABEL author="dariocurr@gmail.com" maintainer="dariocurr@gmail.com" version="0.0.1"

# update apt
RUN apt-get update \
    && apt upgrade -y \
    && export DEBIAN_FRONTEND=noninteractive

# add zsh configuration
COPY .devcontainer/.zshrc .

# install Maven or Gradle
ARG INSTALL_MAVEN="true"
ARG MAVEN_VERSION="3.6.3"
ARG INSTALL_GRADLE="false"
ARG GRADLE_VERSION=""
RUN if [ "${INSTALL_MAVEN}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install maven \"${MAVEN_VERSION}\""; fi \
    && if [ "${INSTALL_GRADLE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install gradle \"${GRADLE_VERSION}\""; fi