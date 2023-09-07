pipeline {
  agent any

  stages {
      stage ('Build and push docker image') {
        steps {
          script {
            // login to docker hub
            withDockerRegistry([credentialsId: 'dockerhub', url: 'https://registry.hub.docker.com']) {
              // build docker image
              def customImage = docker.build("owolabialiu/jenkins", 'Docker/.')
            }
          }    
        }      
      }
  
      stage ('install kubectl') {
        steps {
          script {
            sh """
              sudo rm /usr/local/bin/kubectl
              curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
              chmod +x kubectl
              sudo mv kubectl /usr/local/bin/
            """
          }
        }
      }

      stage ('Deploy to kubernetes cluster') {
        steps {
          script {
            sh  'kubectl create -f Deployment.yaml'
            sh  'kubectl apply -f Kubernetes/Service.yaml'
          }
        }
      }
  }
}