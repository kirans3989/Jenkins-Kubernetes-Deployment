pipeline {
  environment {
registry = "kiranks998/react-app"
registryCredential = 'DockerHub-Credentails'
dockerImage = ''
}
  agent any
    stages {

    stage('Checkout Source') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kirans3989/Jenkins-Kubernetes-Deployment.git', credentialsId: 'Github']]])
      }
    }
    stage('Build Image') {
      steps {
        script {
          dockerImage = docker.build("bravinwasike/react-app:latest")
          }
        }
      }
        stage('Push image') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
          dockerImage.push()
          }
        }
      }
    }
      stage('Cleaning up') {
    steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
 }
}
}
