pipeline {
  agent any
    stages {

    stage('Checkout Source') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kirans3989/Jenkins-Kubernetes-Deployment.git', credentialsId: 'Github']]])
      }
    }
      stage('Pull image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'DockerHub-Credentails') {
            docker.image('bravinwasike/react-app:latest>').pull()
          }
        }
      }
    }
  }
}
