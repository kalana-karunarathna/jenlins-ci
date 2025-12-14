pipeline {
  agent any
  // Specify Node.js version configured in Jenkins
  tools {
    nodejs 'node20'
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
          cobertura coberturaReportFile: 'coverage/cobertura-coverage.xml'
        }
      }
    }
  }
}
