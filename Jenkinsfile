#!/usr/bin/env groovy
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
}
