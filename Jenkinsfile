#!/usr/bin/env groovy

node {
  def app

  stage('Build image') {
    app = docker.build('hapi:${env.BUILD_NUMBER}')
  }

  stage('Test') {
    steps {
      app.inside {
        echo 'Testing...'
        sh 'npm test'
      }
    }
  }

  stage('Push image') {
    when {
      branch 'master'
    }
    steps {
      docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
        app.push('${env.BUILD_NUMBER}')
        app.push('latest')
      }
    }
  }
}
