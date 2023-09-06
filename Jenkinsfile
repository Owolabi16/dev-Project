pipeline {
  agent any

  stages {
      stage ('Build and push docker image') {
        steps {
          script {
            // login to docker hub
            docker.withRegistry([credentialsId: 'hub', url: 'https://registry.hub.docker.com']) {
              // build docker image
              def customImage = docker.build("owolabialiu/jenkins", 'Docker/.')

              // push to docker hub
              customImage.push()
            }
          }    
      }
    }

      stage ('Deploy to kubernetes cluster') {
        steps {
          script {
            sh  'kubectl apply -f deployment.yaml'
            sh  'kubectl apply -f service.yaml'
          }
        }
      }
  }
}
