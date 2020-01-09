FROM ubuntu:18.04

WORKDIR /app

#kubectl
COPY kubectl .
RUN chmod +x ./kubectl && \
mv ./kubectl /usr/local/bin/kubectl
#helm
COPY helm-v3.0.2-linux-amd64.tar.gz .
RUN tar -xzvf helm-v3.0.2-linux-amd64.tar.gz  && \
mv linux-amd64/helm /usr/local/bin/helm 
# mkdir .kube && \
# touch .kube/config
# aws-iam-authenticator
COPY aws-iam-authenticator .
RUN chmod +x ./aws-iam-authenticator && \
 mv ./aws-iam-authenticator /usr/local/bin/aws-iam-authenticator && \
# python pip ansible
 apt-get update && apt-get install -y \
    git \
    python-pip \
    python3 \
    python3-pip



RUN pip3 install awscli --upgrade && \
pip install ansible


COPY credentials .
COPY configaws .
RUN mkdir /root/.aws
COPY ./credentials /root/.aws/credentials
COPY ./configaws /root/.aws/config

COPY config .
RUN mkdir /root/.kube && \
 touch /root/.kube/config && \
 mv config /root/.kube/config
COPY k8s.yml .
RUN KUBECONFIG=/root/.kube/config
