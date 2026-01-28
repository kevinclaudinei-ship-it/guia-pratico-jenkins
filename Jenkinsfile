pipeline {
  agent any

  stages {
    stage ('Build docker image') {
      steps {
        script{
          dockerapp = docker.build("k8syns/guia-jenkins:${env.BUILD_ID}", '-f ./src/Dockerfile ./src' ) 
        }
      }
    } 
    
        stage ('Push docker image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            dockerapp.push('latest')
            dockerapp.push("${env.BUILD_ID}")
          }
        }
      }
    }
    
        stage ('Deploy no kubernetes') {
      steps {
        sh 'echo "executando deploy no kubernetes..."'
      }
    }      
  }
}
