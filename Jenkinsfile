pipeline {
  agent any

  stage ('Build and push docker image') {
    steps {
        script {
            // build docker image
            docker.build -t owolabialiu/jenkins Dockerfile

            // push to docker hub
            docker.push owolabialiu/jenkins 
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
