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
              curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.27.4/2023-08-16/bin/linux/amd64/kubectl
              chmod +x ./kubectl  
              sudo mv ./kubectl /usr/local/bin/
              kubectl version --client    
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
