pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t darinpope/dp-alpine:latest .'
      }
    }
    stage('Publish') {
      steps {
        withDockerRegistry([ credentialsId: "darinpope-dockerhub", url: "" ]) {
          sh 'docker push darinpope/dp-alpine:latest'
        }
      }
    }
  }
}