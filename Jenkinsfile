pipeline {
    agent {
        docker { image 'zhangyhgg/cicd:v1' }
    }
    stages {
        stage('Build Static Website') {
            steps {
                dir ('2 static web site'){
                  sh 'pwd'
                  script {
                      def customImage = docker.build("zhangyhgg/hellonode:v2")
                      customImage.push()
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
                    def customImage = docker.build("zhangyhgg/hellonode:v2")
                    customImage.push()
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