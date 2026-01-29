pipeline {
  agent none

  stages {

    stage ('Build docker image') {
      agent { label 'linux' }
      steps {
        script {
          dockerapp = docker.build(
            "k8syns/guia-jenkins:${env.BUILD_ID}",
            '-f ./src/Dockerfile ./src'
          )
        }
      }
    }

    stage ('Push docker image') {
      agent { label 'linux' }
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
      agent { label 'linux' }

      environment {
        tag_version = "${env.BUILD_ID}"
      }

      steps {
        withKubeConfig([credentialsId: 'kubeconfig']) {
          sh '''
            sed -i "s/{{tag}}/${tag_version}/g" ./k8s/deployment.yaml
            kubectl apply -f k8s/deployment.yaml
          '''
        }
      }
    }
  }
}
