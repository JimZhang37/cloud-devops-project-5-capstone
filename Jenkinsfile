def customImage
def buildAgent
pipeline {
    agent none

    stages {
        stage('Build Agent Image') {
            agent any
            steps {
                dir ('3 docker build agent'){
                  script {
                      buildAgent = docker.build("zhangyhgg/cicd")
                  }
                }
            }
        }
        stage('Upload Agent Image') {
            agent any
            steps {

                script {
                  docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                      buildAgent.push("1")
                  }
                }
            }
        }
        stage('Build Static Website') {
            agent any
            steps {
                dir ('2 static web site'){
                  script {
                      customImage = docker.build("zhangyhgg/hellonode")
                  }
                }
            }
        }
        stage('Test Docker Image') {
            agent any
            steps {
                echo 'Hello world!'
                sh 'pwd'
            }
        }
        stage('Upload Docker Image') {
            agent any
            steps {

                script {
                  docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                      customImage.push("1")
                  }
                }
            }
        }
        stage('Deploy Blue Stack') {
            agent {
              docker { image 'zhangyhgg/cicd:1' }
            }
            steps {
                // sh 'echo $KUBECONFIG'
                // sh 'cat /var/jenkins_home/workspace/devops-project-5-capstone_master/.kube/config'
                // sh 'kubectl version'
                dir ('5 helm'){
                  sh 'helm install web2 ./newweb --wait'
                }
            }
        }

        stage('change dns') {
          agent any
          steps {
                sh 'ANSIBLE_LOCAL_TEMP=/var/jenkins_home/workspace/devops-project-5-capstone_master/.ansible/tmp ansible-playbook ./4 ansible/k8s.yml'
                // ansiblePlaybook  playbook: '4 ansible/k8s.yml'
              }
        }
        
    }
}