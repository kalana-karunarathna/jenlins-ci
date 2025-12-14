pipeline {
  agent any
  options { timestamps() }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('CI in Docker (Node 20)') {
      steps {
        bat '''
          docker pull node:20
          docker run --rm ^
            -v "%CD%":/app ^
            -w /app ^
            node:20 ^
            bash -lc "npm ci && npm run lint && npm test"
        '''
      }
    }
  }

  post {
    always {
      junit 'reports/junit.xml'
      archiveArtifacts artifacts: 'reports/**,coverage/**', fingerprint: true
    }
  }
}
