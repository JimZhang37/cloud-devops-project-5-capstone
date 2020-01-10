# cloud-devops-project-5-capstone

# Folders
* static web site
* terraform
* helm
* jenkins


## Created a K8S cluster in EKS by terraform
    * installed terraform client locally
    * found terraform sample code for aws k8s
    * changed kubectl config file locally so it points to aws k8s
    * 

## Questions
* jenkins x uses a different name for configuration file?
* 

## Jenkin 
* when a build server tries to create a docker image, it couldn't find docker command
* this build server uses docker image for workspace
* it's problem to run docker command inside a docker image

## target today:
* create a docker image and upload it to docker hub. Delayed. I tried jenkins and jenkins x. I think jenkins x is a superier solution, but I am stuck in the middle.

## Day 2 (26 Dec, 2019)
I found how to run docker command inside a jenkins, as it's mentioned in jenkins documentation. Given the fact that jenkins x is far more difficult, I decided to turn back to jenkins. 

Therefore, I will follow the instructions by jenkins documentation. I will create a new build server for this project.

When I used the t1 small, the demo failed as the memory is too small.

I changed type to t2 large. The demo can run. In this demo, the jenkins server run inside a container. It also run another container to build different project. So the docker run inside a docker.

### tomorrow jobs:
run docker build and docker 

# Day 3 (27 December 2019)
## Tasks
* build server can upload docker image to docker hub now, in the new build server


# Day 4 (28 December 2019)
## Tasks
* I learnt Ansible yeasterday
* The Blue/Green deployment example in the course uses route 53, loadbalancer, and ec2. When a new stack is installed, the router will switch traffic from ole stack to the new one.
But, the k8s example is not mentioned.

Ansilbe, roles for ansilbe, credentials for aws, should be configured or installed in the jenkins build server.

I installed ansible in my mac. 
* ansible provisioned a ec2 instance. Ansilbe and boto3 are installed in my mac. A playbook is used to run this task.

## Next:
install a ec2 using ansible in pipeline

# Day 5 (29 December, 2019)

## what's the target?

* a pipeline
* using terraform to provision infrastructure; A dockerfile is used to provide an agent with terraform command.
* using ansible to configure the infrastructure
* give k8s cluster service a dns name

# Day 6 (30 December, 2019)
## what's going on today?
* It's not docker in docker. Instead, it's docker siblings.
github hooker to jenkins

* What I can do now:
build a docker image and upload it to docker hub
run a playbook of ansible

Building a docker image which contains ansilbe, kubectl, helm, etc.

If foreground process exits, the docker container will exit. So one way to run a docker container is to 
`docker run -it {image name} bash`

* what I need to do:
using a docker container in a jenkins pipeline
Given a cluster, the helm and ansible can install a container in a cluster.

To provision a cluster in a separate pipeline.

# Day 7, (31 December 2019)
According to a post, I can run kubectl in a pipeline, meaning I don't need helm or ansible to deploy a new application. I can also control a loadbalancer to fulfill blue/green deployment. This article verifies my first hypothesis that the most important thing is the build language, like groovy. 

# Day 8, (1 January 2020)
* build a static website for this case. It shows a sentence about blue or green.

* tomorrow
build a k8s cluster and run this static website as loadbalancer service.
use ansible to point dns to the loadbalancer
run a new loadbalancer service for green 
* commands:
docker run -it --rm alpine /bin/ash
docker exec -it <container name> /bin/ash
docker run -d --name <container name> -p 80:80 <docker image name>

# Day 9 (2 January 2020)
## Completed:
built a k8s cluster with terraform
using helm to deploye a static website with loadbalancer service type
using helm to deploye a second website with loadbalancer, 2 classic loadbalancer in aws were created

# Day 10 (3 January 2020)
## Completed
tried ansible playbook, roles, etc..
an interesting way to get ansible result is to registe it. Maybe I can use it to save loadbalancer url.
I downloaded istio and it's another solution to blue/green deployment
As one web article pointed out, it's easy to do blue/green with kubectl, but hard to automate this process.

# Day 11 (4 January 2020)
## Completed
Ansible with register value
ansible with dynamic inventory for aws
ansible launch ec2 instance /restart ec2 instance

docker can restart after vm reboots. docker run --restart==always

can I assign the public ip of a new ec2 to a dns hostname? yes, you can

I can assign cname of loadbalancer service's url to cname of route 53

I can use helm install --wait to install a chart and it returns after a loadbalancer is ready.

## conclution
I finished
1 terraform create k8s cluster/ destroy cluster
2 static web site, create docker and upload it to docker hub
3 docker build agent, install ansible, helm in a docker image
4 ansible, change cname, a record in dns. start an ec2 instance, get loadbalancer service's loadbalancer address
5 helm, create a chart and deploy the  chart to a cluster

## Todo
ingredients are ready. It's time to put them in 2 pipelines. Or 3.

1, it's a pipeline to create k8s cluster and destroy it.
2, it's a pipeline for blue stack. It doesn't need to think about swap 2 stacks, so it's simpler. 
3, it's a pipeline for blue/green deployment. 

# Day 12 (5 January 2020)
## Completed:
the first part of blue stack is to build a docker image and upload it to docker hub.

## Todo
the second part of blue stack, is to use helm to deploy it.

# Day 13
install aws, python, pip, (python3, pip3), terraform, kubectl, aws-iam-authenticator and helm in build server

grant a priviledged role to build server so that it can run aws cli.

in terraform, i have to type yes. what can i do in ansible

# Day 15 (7 January 2020)
# completed
ansible script to provision build server and k8s cluster

# todo
blue stack deployment

green stack deployment

# Day 16 (8 Juanry 2020)
To connect to a cluster, the pipeline has to have kubectl and the cluster's credentials. But eks's credentials are different. My conclution is I need to install my jenkins build server inside a k8s cluster. The pipeline doesn't need eks credentials once it's running inside a cluster.

1 create a cluster with terraform
2 use helm v3 to install a jenkins in the cluster
value file used to specify very plugins needed, such as blueocean
3 create a docker credentials for docker up upload
4 install docker plugins in jenkins
5 run the first half of blue deployment, before kubectl.
6 run the second half of the blue deployment, with kubectl
aws role?


## Retrun to traditional way
I decided to return to the old way, which is a jenkins in a EC2 and a independent k8s cluster created by terraform.

To provide kubectl credentials, I created environment varialbe, KUBECONFIG, in jenkins and I put kubeconfiguration file in git hub.

To provide aws credentials, I also used jenkins environment varialbes.

I also created a build agent docker image with all neccesary tools. But one important thing, the agent is not using ubuntu or root. Therefore, I need to put these tools in $PATH specified locations. I once put aws_authentication_file in a new place, but it doesn't work.


# 9 J
installed ansible etc in jenkinsci:blueocean
in docker run -u, i can use root account to run the container

# 11 J
kubeconfig can include more than one path, separated by ":"
the job is done. I submitted this morning.
