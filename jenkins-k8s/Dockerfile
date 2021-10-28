FROM jenkins/jenkins:lts-alpine

USER root

COPY security.groovy /usr/share/jenkins/ref/init.groovy.d/

# Need awscli to get jenkins configuration from S3
# RUN apk add --no-cache python3 && pip3 install awscli

RUN apk add --no-cache python3 py3-pip \
    && pip3 install --upgrade pip \
    && pip3 install --no-cache-dir awscli \
    && rm -rf /var/cache/apk/*

RUN aws --version

USER jenkins

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

COPY ./master-entrypoint.sh /usr/bin/entrypoint

ENTRYPOINT ["/usr/bin/entrypoint"]
