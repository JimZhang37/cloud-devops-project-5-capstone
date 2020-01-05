pipeline {
    agent none
    stages {
        stage('Build Static Website') {
            agent any
            steps {
                dir ('2 static web site'){
                  sh 'pwd'
                  script {
                      def customImage = docker.build("zhangyhgg/hellonode:v2")

                  }
                }
                echo 'Hello world!'
                sh 'pwd'
            }
        }
        stage('Test Docker Image') {
            agent {
              docker { image 'zhangyhgg/cicd:v1' }
            }
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
                      app.push("v2")
                  }
                }
            }
        }
        // stage('Deploy Blue Stack') {
        //     steps {
        //         //kubectl and credentials
        //         sh 'helm install web ./5\ helm/staticweb --wait'
        //         echo 'helm deploy!'
        //         sh 'ansible-playbook ./4\ ansible/k8s.yml'
        //     }
        // }
    }
}