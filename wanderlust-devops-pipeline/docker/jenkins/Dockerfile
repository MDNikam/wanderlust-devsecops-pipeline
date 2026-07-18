FROM jenkins/jenkins:lts-jdk21

USER root

ENV DEBIAN_FRONTEND=noninteractive

# Install essential packages
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    unzip \
    zip \
    jq \
    gnupg \
    ca-certificates \
    lsb-release \
    libatomic1 \
    python3 \
    python3-pip

# Install NodeJS 22 LTS
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - && \
    apt-get install -y nodejs

# Install Docker CLI
RUN apt-get update && \
    apt-get install -y docker.io

USER jenkins