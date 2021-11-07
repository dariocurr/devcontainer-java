# Load variables
ARG JAVA_VERSION

# Choice image
FROM mcr.microsoft.com/vscode/devcontainers/java:0-${JAVA_VERSION}

# Update apt
RUN apt-get update \
    && apt upgrade -y \
    && export DEBIAN_FRONTEND=noninteractive

# Install Maven or Gradle
ARG INSTALL_MAVEN
ARG MAVEN_VERSION
ARG INSTALL_GRADLE
ARG GRADLE_VERSION
RUN if [ "${INSTALL_MAVEN}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install maven \"${MAVEN_VERSION}\""; fi \
    && if [ "${INSTALL_GRADLE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install gradle \"${GRADLE_VERSION}\""; fi