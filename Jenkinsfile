pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = '621917999036.dkr.ecr.ap-northeast-2.amazonaws.com' // ECR URL
        IMAGE_NAME = 'jenkins_web' // Docker 이미지 이름
        AWS_CREDENTIAL_NAME = 'AWS-Jenkins' // AWS 자격 증명 이름
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // cleanup current user docker credentials
                   // sh 'rm -f ~/.dockercfg ~/.docker/config.json || true'

                    // configure registry
                    docker.withRegistry('https://${DOCKER_REGISTRY}', 'ecr:AWS-Jenkins') {
                        // build image
                        def customImage = docker.build("${IMAGE_NAME}:${env.BUILD_ID}")

                        // push image
                        customImage.push()
                        customImage.push("latest")
                    }
                }
            }
        }
    }
}
