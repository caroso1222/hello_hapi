#!/usr/bin/env groovy

pipeline {

    agent {
        dockerfile true
    }

    stages {
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }
    }
}
