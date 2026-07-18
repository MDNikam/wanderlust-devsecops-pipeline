FROM jenkins/jenkins:lts-jdk21

USER root

RUN apt-get update && \
    apt-get install -y \
    docker.io \
    curl \
    unzip \
    git && \
    apt-get clean

USER jenkins