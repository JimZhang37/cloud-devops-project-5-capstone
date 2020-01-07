# Ansible 
* dynamic inventory for aws
/etc/ansible/hosts is a py file to fetch inventory dynamicly.

don't use brew to install ansible. use pip instead. Or you will not be able to install dynamic inventory correctly.

* I can setup my jenkins build server with ansible next time. For example, I can run docker container when it starts.

* I can use register to get the return value of a task. For example, after I provisioned a server, its return value inclues its ip and etc.

ansible all -i hosts -u vagrant -m ping
ansible all -i hosts -u vagrant -m setup
ansible webserver -i hoost -u vagrant -m yum -a "name=httpd state=present" -b
ansible-playbook -i hosts playbook.yml

In a playbook, you can configure remote user and host. 