pipeline {

  environment {
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

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
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