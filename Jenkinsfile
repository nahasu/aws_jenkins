app = docker.build("621917999036.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins_web")


docker.withRegistry('https://621917999036.dkr.ecr.ap-northeast-2.amazonaws.com', 'AWS-Jenkin')


  
node {
     stage('Clone repository') {
         checkout scm
     }

     stage('Build image') {
         app = docker.build("621917999036.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins_web")
     }

     stage('Push image') {
         sh 'rm  ~/.dockercfg || true'
         sh 'rm ~/.docker/config.json || true'
         
         docker.withRegistry('https://621917999036.dkr.ecr.ap-northeast-2.amazonaws.com', 'AWS-Jenkins') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
     }
  }
