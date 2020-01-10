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
        stage('Test Static Website') {
            agent any
            steps {
                dir ('2 static web site'){
                  sh 'html_lint.py --disable=optional_tag *.html'
                  // sh 'tidy -q -e *.html'
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
        // stage('Test Docker Image') {
        //     agent any
        //     steps {
        //         echo 'Hello world!'
        //         sh 'pwd'
        //     }
        // }
        stage('Upload Docker Image') {
            agent any
            steps {

                script {
                  docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                      customImage.push("2")
                  }
                }
            }
        }
        stage('Deploy Green Stack') {
            agent {
              docker { image 'zhangyhgg/cicd:1' }
            }
            steps {
                sh 'pwd'
                sh 'echo $WORKSPACE'
                sh 'echo KUBECONFIG=${WORKSPACE}/.kube/config > abcfile'
                sh 'echo $KUBECONFIG'
                // sh 'cat /var/jenkins_home/workspace/devops-project-5-capstone_master/.kube/config'
                // sh 'kubectl config --kubeconfig /var/jenkins_home/workspace/devops-project-5-capstone_greenversion/.kube/config'
                dir ('5 helm'){
                  sh 'helm install web3 ./newweb --wait'
                }
            }
        }

        stage('change dns') {
            agent any
          steps {
                //sh 'ANSIBLE_LOCAL_TEMP=/var/jenkins_home/workspace/devops-project-5-capstone_master/.ansible/tmp ansible-playbook ./4 ansible/k8s.yml'
                dir ('4 ansible'){
                  
                  sh 'ansible --version'
                  sh 'which ansible'
                  ansiblePlaybook  playbook: 'k8s.yml'
                }
              }
        }
        
    }
}