pipeline {
  agent none
  options { 
    buildDiscarder(logRotator(numToKeepStr: '2'))
    skipDefaultCheckout true
  }
  triggers {
    eventTrigger simpleMatch('hello-api-deploy-event')
  }
  stages {
    stage('Test') {
      agent {
        kubernetes {
          label 'nodejs-app-pod'
          yamlFile 'nodejs-pod.yml'
        }
      }
      steps {
        checkout scm
        container('nodejs') {
          echo 'Hello World!'   
          sh 'node --version'
        
        }
      }
    }
    stage('Build and Push Image'){
      when {
        beforeAgent true
        branch 'master'
      }
      steps {
        echo "TODO - build and push image" 
      }
    }
    stage('Deploy') {
      when {
        beforeAgent true
        beforeInput true
        branch 'master'
      }
      input {
        message "Should we continue?"
      }
      steps {
        echo "Continuing with deployment"
      }
    }
  }
}
