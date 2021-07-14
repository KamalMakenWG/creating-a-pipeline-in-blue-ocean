pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          environment {
            CI = 'true'
          }
          steps {
            sh './jenkins/scripts/test.sh'
          }
        }

        stage('') {
          steps {
            p4sync(credential: 'au1-perforce-02:1666', depotPath: '//enclave/proto/main/enclave/Scripts/Sydney/Automation/DMS/', charset: 'None')
          }
        }

      }
    }

  }
}