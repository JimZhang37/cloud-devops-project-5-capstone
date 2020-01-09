# The agent of jenkins build server
## Features
The jenkins build server uses a docker container agent as it can install helm, ansible in the docker image.

## how to test the image
run
aws s3 ls
kubectl version
ansible-playbook k8s.yml