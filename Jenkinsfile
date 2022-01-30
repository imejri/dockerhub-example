
pipeline {
  agent { label 'centos' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-issam')
    ARTIFACTORY_SERVER='test.pme.com'
    RUNNING_VERSION='1.2.0'
  }
  stages {
    stage('Build') {
      steps {
        sh './jenkins/build.sh'
      }
    }
    stage('print variable') {
      environment {
        file="config/file"
      }
      steps {
        script {
          echo "the file is ${file}"
        sh './jenkins/variable.sh'
        } //script
      } //steps
    } // stage
    
    stage('Login') {
      steps {
        sh './jenkins/login.sh'
      }
    }
    stage('Push') {
      steps {
        sh './jenkins/push.sh'
      }
    }
  }
  post {
    always {
      sh './jenkins/logout.sh'
    }
  }
}
