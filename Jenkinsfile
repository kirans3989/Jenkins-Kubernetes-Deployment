pipeline { 
    environment { 
        registry = "kiranks998/react-app" 
        registryCredential = 'DockerHub-Credentails' 
        dockerImage = '' 
    }

    agent any 
    stages {       
        stage('Cloning our Git') { 
          steps { 
             checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kirans3989/Jenkins-Kubernetes-Deployment.git', credentialsId: 'Github']]])
          }
      } 
      stage('Building our image') { 
          steps { 
              script { 
                  dockerImage = docker.build registry + ":$BUILD_NUMBER" 
              }
          } 
      }
      stage('Deploy our image') { 
          steps { 
              script { 
                  docker.withRegistry( '', registryCredential ) { 
                      dockerImage.push() 
                  }
              } 
          }
      } 
      stage('Cleaning up') { 
          steps { 
              sh "docker rmi $registry:$BUILD_NUMBER" 
          }
      }
  }

}
