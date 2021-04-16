pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        docker.build('darinpope/dp-alpine-with-plugin:latest').push()
      }
    }
  }
}