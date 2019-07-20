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
        sh """#!/bin/bash -e
          docker-compose build app
        """
    }

    stage('Build an image with Tests') {
        sh """#!/bin/bash -e
          docker-compose build robottests
        """
    }

    stage('Run Docker Compose') {
        sh """#!/bin/bash -e
           docker-compose run --rm robottests  ./wait-for-it.sh -t 15 chromenode:5555 -- robot -d reports --variablefile variables/config.py --variable BROWSER:chrome tests/
        """
    }    
  }
}
