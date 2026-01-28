pipeline {
  agent any

  stages {
    stage ('Build docker image') {
      steps {
        sh 'echo "executando build..."'
      }
    } 
    
        stage ('Push docker image') {
      steps {
        sh 'echo "executando push..."'
      }
    }
    
        stage ('Deploy no kubernetes') {
      steps {
        sh 'echo "executando deploy no kubernetes..."'
      }
    }      
  }
}
