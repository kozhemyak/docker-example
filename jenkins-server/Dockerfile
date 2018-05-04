FROM jenkins/jenkins:lts-alpine

LABEL maintainer="Nikolay Kozhemyak <nkozhemyak@gmail.com>"

ENV JAVA_OPTS "-Djenkins.install.runSetupWizard=false"

USER root

RUN echo "jenkins ALL= NOPASSWD: ALL" >> /etc/sudoers

# Minimize size
RUN rm -rf /var/lib/apt/lists/* \
    /var/cache/apk/* \
    /usr/share/man \
    /tmp/*

USER jenkins