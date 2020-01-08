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
                dir('.kube'){
                  sh 'cat config'
                }
                sh 'echo $PATH'
                sh 'echo $KUBECONFIG'
                sh 'cat /app/.kube/config'

                sh 'kubectl config view'

                // dir ('5 helm'){
                //   sh 'helm install web staticweb --wait'
                // }
                
                echo 'helm deploy!'
                sh 'ansible --version'
                //sh 'ansible-playbook ./4\ ansible/k8s.yml'
            }
        }
    }
}