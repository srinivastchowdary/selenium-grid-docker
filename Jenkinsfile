#!groovy
node('master') {
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
          docker-compose build app
        """
    }

    stage('Build an image with Tests') {
        sh """
          docker-compose build robottests
        """
    }

    stage('Run Docker Compose') {
        sh """#!/bin/bash -e
          docker-compose -p my_unique_project up -d --build
          docker-compose -p my_unique_project exec robottests ./wait-for-it.sh -t 15 selenium_hub:4444 -- robot -d reports  --variablefile variables/config.py  --variable BROWSER:firefox tests/
        """
    }

    stage('Stop all containers') {
        sh """
          docker-compose down
        """
    }
  }
}
