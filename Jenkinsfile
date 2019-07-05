pipeline {
  agent any

  environment {
    TAG = "demo_${env.BRANCH_NAME}_${env.BUILD_NUMBER}"
  }

  stages {
    stage("Checkout") {
      steps {
        checkout scm
      }
    }
    stage("Cleaning and preparing") {
      steps {
        sh """#!/bin/bash -e
          git clean -dfx
          mkdir reports
        """
      }
    }
  }
}
