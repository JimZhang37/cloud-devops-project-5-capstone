FROM ubuntu:18.04

WORKDIR /app
COPY helm-v3.0.2-linux-amd64.tar.gz .
COPY kubectl .
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl
RUN apt-get update && apt-get install -y  ansible 
# RUN wget https://get.helm.sh/helm-v3.0.2-linux-amd64.tar.gz 
RUN tar -xzvf helm-v3.0.2-linux-amd64.tar.gz 
RUN mv linux-amd64/helm /usr/local/bin/helm 
RUN mkdir .kube 
RUN touch .kube/config