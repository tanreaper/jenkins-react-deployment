pipeline {

  environment {
    PATH = "/usr/local/bin:$PATH"
    dockerimagename = "tanreaper/react-app"
    dockerImage = ""
  }
  agent any
  stages {
    stage('Git checkout') {
      steps {
        git(branch: 'main', 
            url: "https://github.com/tanreaper/jenkins-react-deployment.git")
        }
    }
    stage('Docker Build and Push') {
      steps {
        script{
          withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:'dockerhub-credential', usernameVariable: 'DOCKER_USERNAME', passwordVariable:'DOCKER_PASSWORD']]) {
            sh "$DOCKER_USERNAME"
            sh "$DOCKER_PASSWORD"
          }
        }
      }
    }   
  }

}