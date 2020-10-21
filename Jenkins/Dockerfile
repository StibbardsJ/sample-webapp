FROM jenkins/jenkins

ENV JAVA_OPTS "-Djenkins.install.runSetupWizard=false"
ENV CASC_JENKINS_CONFIG /var/jenkins_conf

ENV DOCKER_CHANNEL stable
ENV DOCKER_VERSION 19.03.12
USER root
# DOCKER_GID should correspond to the group id of the docker group. You can check it on Linux systems with 'getent group docker'
ENV DOCKER_GID=1001

# Get kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl

USER jenkins

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
COPY jenkins.yaml /var/jenkins_conf/jenkins.yaml
RUN xargs /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt