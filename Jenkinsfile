docker.withRegistry('https://621917999036.dkr.ecr.ap-northeast-2.amazonaws.com', 'AKIAZBTJTR66FN3PO4OT') {
    node {
        stage('Clone repository') {
            checkout scm
        }

        stage('Build image') {
            // Dockerfile이 Jenkinsfile과 같은 경로에 있으므로 별도의 경로 지정이 필요하지 않음
            app = docker.build("621917999036.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins_web")
        }

        stage('Push image') {
            sh 'rm  ~/.dockercfg || true'
            sh 'rm ~/.docker/config.json || true'
            
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
