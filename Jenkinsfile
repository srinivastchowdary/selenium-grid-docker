#!groovy
node {
  wrap([$class: 'AnsiColorBuildWrapper', colorMapName: 'xterm']) {
    stage("Checkout") {
      checkout scm
    }
     stage("Cleaning and preparing") {
      sh '''#!/bin/bash -e
        git clean -dfx
        mkdir reports
      '''
    }
     stage('Build an image with App') {
        sh """
          docker-compose build app:{BUILD_NUMBER}
        """
    }
  }
}
