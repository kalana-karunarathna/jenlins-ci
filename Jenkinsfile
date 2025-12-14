pipeline {
  agent {
    docker {
      image 'node:20'
      args '-u root:root'
    }
  }
  
  options { timestamps() }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install') {
      steps {
        sh 'npm ci || npm install'
      }
    }
    stage('Lint') {
      steps {
        sh 'npm run lint'
      }
   }


    stage('Test') {
      steps {
        sh 'npm test'
      }
      post {
        always {
          junit 'reports/junit.xml'
          archiveArtifacts artifacts: 'reports/junit.xml', fingerprint: true
          
        }
      }
    }
  }
}
