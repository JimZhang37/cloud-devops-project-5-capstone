pipeline {
    agent {
        docker { image 'zhangyhgg/cicd:v1' }
    }
    stages {
        stage('Build Static Website') {
            steps {
                dir ('2 static web site')
                sh 'pwd'
                echo 'Hello world!'
            }
        }
    }
}