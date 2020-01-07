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
              docker { image 'zhangyhgg/cicd:2' }
            }
            steps {
                //kubectl and credentials
                // echo $PATH
                sh 'kubectl version'
                // sh 'helm install web ./5 helm/staticweb --wait'
                // echo 'helm deploy!'
                // sh 'ansible-playbook ./4\ ansible/k8s.yml'
            }
        }
    }
}