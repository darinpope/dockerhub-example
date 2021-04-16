pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('darinpope-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t darinpope/dp-alpine:latest .'
      }
    }
    stage('Scan') {
      steps {
        sh 'docker scan --accept-license --dependency-tree darinpope/dp-alpine:latest'
      }
    }
    stage('Publish') {
      steps {
        sh '''
          echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
          docker push darinpope/dp-alpine:latest
          docker logout
        '''
      }
    }
  }
}