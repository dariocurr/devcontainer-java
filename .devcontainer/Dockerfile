# select image
ARG JAVA_VERSION
FROM mcr.microsoft.com/vscode/devcontainers/java:0-${JAVA_VERSION}

# update apt
RUN apt-get update \
    && apt upgrade -y \
    && export DEBIAN_FRONTEND=noninteractive

# add zsh configuration
COPY .devcontainer/.zshrc .

# install Maven or Gradle
ARG INSTALL_MAVEN
ARG MAVEN_VERSION
ARG INSTALL_GRADLE
ARG GRADLE_VERSION
RUN if [ "${INSTALL_MAVEN}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install maven \"${MAVEN_VERSION}\""; fi \
    && if [ "${INSTALL_GRADLE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install gradle \"${GRADLE_VERSION}\""; fi