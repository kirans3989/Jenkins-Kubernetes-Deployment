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
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
            docker.image('bravinwasike/react-app:latest>').pull()
          }
        }
      }
    }

    stage('Build image') {
      steps {
        script {
          docker.build('kiranks998/react-app:latest>', '.').push()
        }
      }
    }

    stage('Push image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'DockerHub-Credentails') {
            docker.image('kiranks998/react-app:latest').push()
          }
        }
      }
    }
     stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }
  }
}
