pipeline {
    agent {
        docker { image 'zhangyhgg/cicd:v1' }
    }
    stages {
        stage('Build Static Website') {
            steps {
                dir ('2 static web site'){
                  sh 'pwd'
                  sh 'helm version'
                  sh 'echo $PATH'
                }
                
                echo 'Hello world!'
                sh 'pwd'
            }
        }
        stage('Build Docker Image') {
            steps {
                dir ('3 docker build agent'){
                  sh 'pwd'
                  sh 'ls'
                  sh 'docker version'
                  sh 'ls'
                }
                
                echo 'Hello world!'
                sh 'pwd'
            }
        }
    }
}