pipeline {
  agent any
  environment {
    WEBROOT = '/var/www/portfolio'
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Static site - no build step required'
      }
    }

    stage('Deploy') {
      steps {
        sh '''
          set -e
          # ensure webroot exists
          mkdir -p ${WEBROOT}
          # copy files from workspace to webroot (exclude .git)
          rsync -av --delete --exclude='.git' "${WORKSPACE}/" "${WEBROOT}/"
        '''
      }
    }
  }
  post {
    success {
      echo "Deployed to ${WEBROOT}"
    }
    failure {
      echo "Pipeline failed - check console output"
    }
  }
}
