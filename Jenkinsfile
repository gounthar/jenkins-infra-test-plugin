pipeline {
  agent any
  tools {
        jdk 'jdk19' 
        mvn "3.8.6'
  }
  stages {
    stage('Checkout') {
        steps {
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jenkinsci/jenkins-infra-test-plugin.git/']]])
      }
    }
    stage('Shell script 0') {
      steps {
        withCredentials([string(credentialsId: 'GITHUB_CREDENTIALS_PSW', variable: 'GITHUB_CREDENTIALS_PSW')]) {
          sh '''
                java --version
                mvn clean verify -Denforcer.skip=true
          '''
        }

      }
    }

  }
  options {
    timeout(time: 66, unit: 'MINUTES')
  }
}
