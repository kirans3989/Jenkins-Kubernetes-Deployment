pipeline {
  agent any
    stages {
      
  stage('Checkout Source') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kirans3989/Jenkins-Kubernetes-Deployment.git', credentialsId: 'Github']]])
      }
    }
    
    stage('Build image') {
      steps {
        script {
       dockerImage = docker.build("bravinwasike/react-app:latest")
    }
      }
 stage('Push image') {
   steps {
        script {
        withDockerRegistry([ credentialsId: "DockerHub-Credentails", url: "https://registry.hub.docker.com" ]) {
        dockerImage.push()
        }
        }
   }
    }    
  }
}
