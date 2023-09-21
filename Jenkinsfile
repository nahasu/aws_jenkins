pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("621917999036.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins_web")
                    docker.withRegistry('https://621917999036.dkr.ecr.ap-northeast-2.amazonaws.com', 'AWS-Jenkins') {
                        dockerImage.push("${env.BUILD_NUMBER}")
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}
