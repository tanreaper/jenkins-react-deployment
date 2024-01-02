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
          withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable:'DOCKER_PASSWORD']]) {
            sh "docker build -t tanreaper/react-app ."
            sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
            sh "docker push tanreaper/react-app"
          }
        }
      }
    } 
    stage('Deploy to Minikube') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl apply -f service.yaml'
      }
    }  
  }

}