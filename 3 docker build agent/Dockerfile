FROM ubuntu:18.04

WORKDIR /app
COPY helm-v3.0.2-linux-amd64.tar.gz .
RUN apt-get update && apt-get install -y  ansible 
# RUN wget https://get.helm.sh/helm-v3.0.2-linux-amd64.tar.gz 
RUN tar -xzvf helm-v3.0.2-linux-amd64.tar.gz 
RUN mv linux-amd64/helm /usr/local/bin/helm 
RUN mkdir .kube 
RUN touch .kube/config

RUN apt-get install docker-ce docker-ce-cli containerd.io
  