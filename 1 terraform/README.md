# Provisioning a k8s cluster with terraform

## How to provision a cluster
step 1: terraform init
step 2: terraform output kubeconfig>~/.kube/config
step 3: terraform output config_map_aws_auth > configmap.yml
kubectl apply -f configmap.yml
step 4: kubectl get nodes -o wide
step 5: terraform destroy

https://aws.amazon.com/blogs/startups/from-zero-to-eks-with-terraform-and-helm/



## EKS Getting Started Guide Configuration

This is the full configuration from https://www.terraform.io/docs/providers/aws/guides/eks-getting-started.html

See that guide for additional information.

NOTE: This full configuration utilizes the [Terraform http provider](https://www.terraform.io/docs/providers/http/index.html) to call out to icanhazip.com to determine your local workstation external IP for easily configuring EC2 Security Group access to the Kubernetes master servers. Feel free to replace this as necessary.
