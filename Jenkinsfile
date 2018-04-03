#!/usr/bin/env groovy

node {
  def app

  stage("Clone") {
    checkout scm
  }

  stage("Build") {
    app = docker.build("caroso1222/hapi")
  }

  stage("Test") {
    app.inside {
      echo "Testing..."
      sh "npm test"
    }
  }

  stage("Push") {
    docker.withRegistry("https://registry.hub.docker.com", "docker-hub-credentials") {
      app.push("${env.BUILD_ID}")
      app.push("latest")
    }
  }

  stage("Deploy") {
    sh "ssh root@159.65.180.234 \"docker stop hapi_0 && \
        docker rm hapi_0 && \
        docker pull caroso1222/hapi:latest && \
        docker run -d --name=hapi_0 -p 80:3000 caroso1222/hapi:latest\""
  }
}
