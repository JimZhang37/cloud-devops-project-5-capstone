folder:
	mkdir roles
	cd roles


# ad-hoc commands

ping:
	ansible all -m ping

uptime:
	ansible web -m command -a "uptime"

setup:
	ansible localhost -m setup

# playbook

play:
	ansible-playbook -i hosts site.yml

role:
	ansible-playbook -i hosts site2.yml

aws: 
	ansible-playbook aws.yml

awsstop: 
	ansible-playbook aws-stop.yml

refresh:
	/etc/ansible/hosts --refresh-cache

test:
	ansible all --list-hosts

k8s:
	ansible-playbook k8s.yml

terraform:
	ansible-playbook terraform.yml

terraformdelete:
	ansible-playbook terraforminfo.yml

auth:
	echo LSuperLongBase64EncodedString== | base64 -d > ca.crt

crt:
	