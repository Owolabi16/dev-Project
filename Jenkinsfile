pipeline {
  agent any

  stages {
      stage ('Build and push docker image') {
        steps {
          script {
            // login to docker hub
            withDockerRegistry([credentialsId: 'hub', url: 'https://registry.hub.docker.com']) {
              // build docker image
              def customImage = docker.build("owolabialiu/jenkins", 'Docker/.')
            }
          }    
      }
    }

      stage ('Deploy to kubernetes cluster') {
        steps {
          script {
            sh  'kubectl apply -f Kubernetes/deployment.yaml'
            sh  'kubectl apply -f Kubernetes/service.yaml'
          }
        }
      }
  }
}
