pipeline {
  agent any

  stage ('Build and push docker image') {
    steps {
        script {
            // build docker image
            def customImage = docker.build("owolabialiu/jenkins", 'Docker/.')

            // push to docker hub
            customImage.push()
        }    
    }
  }

  stage ('Deploy to kubernetes cluster') {
    steps {
        script {
            kubectl apply -f deployment.yaml
            kubectl apply -f service.yaml
        }
    }
  }
}


def customImage = docker.build("owolabialiu/jenkins:${env.BUILD_NUMBER}", 'Docker/Dockerfile')