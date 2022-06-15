FROM alpine:latest

LABEL maintainer="m4rkus@engineers4cloud" description="ultimate-cli" version="1.2.2"

# Versions
ENV TERRAFORM_VERSION=1.2.2

# Tool Envs
ENV USER_HOME_DIR=/opt/ultimate-cli
ENV HOME=/opt/ultimate-cli
#ENV CDK_HOME=/opt/ultimate-cli/cdk

WORKDIR /opt/ultimate-cli

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

# install whats available from alpine repos
RUN apk upgrade --available --no-cache \
&& apk add --no-cache \
    apk-tools \
    curl \
    aws-cli \
    nodejs \
    jq \
    wget \
    bash \
    git \
    zip \
    python3 \
    python3-dev \
    py3-pip \
    gcc \
    openssl
  
# install terraform
RUN wget -q https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
&& unzip -d /tmp terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
&& mv /tmp/terraform /usr/local/bin \
&& chmod +x /usr/local/bin/terraform

RUN ln -sf python3 /usr/bin/python \
&& pip install --no-cache-dir pipenv \
&& chgrp -R 0 /opt/ultimate-cli \
&& chmod -R g=u /opt/ultimate-cli
   
# set bash as default shell
SHELL ["/bin/bash", "-c"]

USER 1000
