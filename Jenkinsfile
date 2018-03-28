#!/usr/bin/env groovy

node {
  def app

  stage('Clone') {
        checkout scm
    }

  stage('Build') {
    app = docker.build('hapi:${env.BUILD_ID}')
  }

  stage('Test') {
    steps {
      app.inside {
        echo 'Testing...'
        sh 'npm test'
      }
    }
  }

  stage('Push') {
    when {
      branch 'master'
    }
    steps {
      docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
        app.push('${env.BUILD_ID}')
        app.push('latest')
      }
    }
  }
}
