# docker build -t jatindesai/jenkins:lts-alpine .
# adding jenkins user with sudo access to be able to access docker cli
# adding kubectl
# adding jenkins plugins

FROM jenkins/jenkins:lts-alpine
MAINTAINER Jatin Desai <jatindesai@yahoo.com>

USER root
RUN apk update \
      && apk add sudo curl \
      && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
RUN addgroup -S docker
RUN adduser jenkins docker

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.10.0/bin/linux/amd64/kubectl
RUN chmod +x kubectl
RUN mv ./kubectl /usr/local/bin

USER jenkins
COPY plugins1.txt /usr/share/jenkins/plugins1.txt
COPY plugins2.txt /usr/share/jenkins/plugins2.txt
COPY plugins3.txt /usr/share/jenkins/plugins3.txt
COPY plugins4.txt /usr/share/jenkins/plugins4.txt
COPY plugins5.txt /usr/share/jenkins/plugins5.txt

RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins1.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins2.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins3.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins4.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins5.txt
