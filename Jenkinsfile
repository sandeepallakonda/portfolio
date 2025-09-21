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
          # ensure webroot exists
          mkdir -p ${WEBROOT}
          # copy files from workspace to webroot (exclude .git)
          rsync -r --delete --exclude='.git' "${WORKSPACE}/" "${WEBROOT}/"
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
