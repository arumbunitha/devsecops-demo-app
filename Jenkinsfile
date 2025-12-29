pipeline {
  agent any

  environment {
    APP_NAME = "devsecops-demo"
    IMAGE_TAG = "1.0.${BUILD_NUMBER}"
  }

  stages {

    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/arumbunitha/devsecops-demo-app.git'
      }
    }

    stage('Build') {
      steps {
        sh '/opt/homebrew/bin/mvn clean package'
      }
    }

    stage('Docker Build') {
      steps {
        sh '/usr/local/bin/docker --version'
        sh "/usr/local/bin/docker build -t ${APP_NAME}:${IMAGE_TAG} ."
      }
    }

    stage('Deploy (Mock)') {
      steps {
        sh 'echo "Deploying application (mock stage)"'
      }
    }
  }

  post {
    success {
      echo 'Pipeline completed successfully'
    }
    failure {
      echo 'Pipeline failed'
    }
  }
}

