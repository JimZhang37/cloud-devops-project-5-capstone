def customImage
pipeline {
    agent any

    stages {
        stage('Build Static Website') {
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

            steps {
                echo 'Hello world!'
                sh 'pwd'
            }
        }
        stage('Upload Docker Image') {

            steps {

                script {
                  docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                      customImage.push("2")
                  }
                }
            }
        }
        stage('Deploy Blue Stack') {

            steps {
                //kubectl and credentials
                // echo $PATH
                sh '/usr/bin/kubectl version'
                // sh 'helm install web ./5 helm/staticweb --wait'
                // echo 'helm deploy!'
                // sh 'ansible-playbook ./4\ ansible/k8s.yml'
            }
        }
    }
}