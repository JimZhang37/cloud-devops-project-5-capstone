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
                      customImage.push("1")
                  }
                }
            }
        }
        stage('Deploy Blue Stack') {
            agent {
              docker { image 'zhangyhgg/cicd:10' }
            }
            steps {
                //kubectl and credentials
                // echo $PATH
                //sh 'eks'
                // sh 'mkdir ~/.kube'
                // dir('.aws'){
                //   sh 'cat config'
                //   sh 'cat credentials'
                // }
                // sh 'echo $PATH'
                // sh 'echo $AWS_CONFIG_FILE'
                // sh 'echo $KUBECONFIG'
                // sh 'cat .kube/config'

                // sh 'kubectl config view'
                sh  'pwd'
                dir ('5 helm'){
                  sh 'helm install web2 ./newweb --wait'
                }
                // sh 'aws configure set region us-east-2 --profile default  '
                // sh 'aws configure set output text --profile default  '
                // sh 'aws configure set aws_access_key_id AKIATJ74JRDZC42DAOGU --profile default  '
                // sh 'aws configure set aws_secret_access_key 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 --profile default  '

                // sh 'aws configure get region --profile default'
                
                // echo 'helm deploy!'
                // sh 'ansible --version'
                dir('4 ansible'){
                  // sh 'ansible-playbook k8s.yml'
                  ansiblePlaybook sudo playbook: 'k8s.yml'
                }
                //sh 'ansible-playbook ./4\ ansible/k8s.yml'
            }
        }
    }
}