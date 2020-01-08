FROM ubuntu:18.04

WORKDIR /app

#kubectl
COPY kubectl .
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl
#helm
COPY helm-v3.0.2-linux-amd64.tar.gz .
RUN tar -xzvf helm-v3.0.2-linux-amd64.tar.gz 
RUN mv linux-amd64/helm /usr/local/bin/helm 
RUN mkdir .kube 
RUN touch .kube/config
# aws-iam-authenticator
COPY aws-iam-authenticator .
RUN chmod +x ./aws-iam-authenticator
RUN mkdir -p $HOME/bin && cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator && export PATH=$HOME/bin:$PATH
RUN echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
# python pip ansible
RUN apt-get update && apt-get install -y \
    git \
    python-pip \
    ansible \
    python3 \
    python3-pip

COPY config .
RUN mkdir /root/.kube
RUN touch /root/.kube/config
RUN mv config /root/.kube/config
COPY k8s.yml .

RUN pip3 install awscli --upgrade

COPY credentials .
COPY configaws .
RUN mkdir /root/.aws
COPY ./credentials /root/.aws/credentials
COPY ./configaws /root/.aws/config

