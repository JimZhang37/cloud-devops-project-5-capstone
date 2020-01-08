def customImage
pipeline {
    agent none

    stages {
        stage('Build Static Website') {
            agent any
            steps {
                dir ('2 static web site'){
                  sh 'pwd'
                  script {
                      customImage = docker.build("zhangyhgg/hellonode")

                  }
                }
                echo 'Hello world!'
                sh 'pwd'
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
                      customImage.push("2")
                  }
                }
            }
        }
        stage('Deploy Blue Stack') {
            agent {
              docker { image 'zhangyhgg/cicd:3' }
            }
            steps {
                //kubectl and credentials
                // echo $PATH
                //sh 'eks'
                // sh 'mkdir ~/.kube'
                dir('.aws'){
                  sh 'cat config'
                  sh 'cat credentials'
                }
                sh 'echo $PATH'
                sh 'echo $KUBECONFIG'
                sh 'cat .kube/config'

                sh 'kubectl config view'
                // sh  'kubectl version'
                // dir ('5 helm'){
                //   sh 'helm install web staticweb --wait'
                // }
                sh 'aws ec2 describe-instances'
                echo 'helm deploy!'
                sh 'ansible --version'
                dir('4 ansible'){
                  sh 'ansible-playbook k8s.yml'
                }
                //sh 'ansible-playbook ./4\ ansible/k8s.yml'
            }
        }
    }
}